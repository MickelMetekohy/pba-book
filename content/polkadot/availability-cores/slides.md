---
title: Deep Dive, Availability Cores
duration: 1 hour
description: The Polkadot Abstraction for Flexible Blockspace Allocation
---

# Deep Dive, Availability Cores

## Deep Dive, Availability Cores

Notes:

Hello!

I'm Bradley Olson

Was student at first Academy

Currently on Parachains Core Team

Will present 3 lectures providing a window into Polkadot core, a slice of where we're at and where we're headed.

First a look at availability cores, the abstraction enabling flexible purchases of blockspace under the umbrella of Polkadot shared security.

Lets get to it

***

### Addressing the Dual Naming

* In the code: Availability core
* Outside the code: Execution core

***

### Overview

* What do availability cores represent?
* How do cores map parachain leases and claims to validator subsets?
* How do cores gate each step of the parachains protocol?
* What advantages do cores give us now?
* What roadmap items do cores accommodate?

***

### Review, Blockspace

> Blockspace is the capacity of a blockchain\
> to finalize and commit operations

Polkadot's primary product is _blockspace_.

***

### Blockspace, Use It or Lose It

Polkadot blockspace is consumed in two ways:

1. When the relay chain validates, includes,\
   and finalizes a parachain block
2. When the capacity to validate a parachain block\
   is left unused and expires

![](../async-backing-deep/img/stopwatch.png)

***

### Availability Core Defined

* Availability cores are the abstraction we use to allocate Polkadot's blockspace.
* Allocated via leases and on-demand claims
* Cores divide blockspace supply into discrete units, 1 parachain block per relay chain block per core
* Why "availability"?
* Why "core"?

![](img/Processor_Cores.jpeg)

Notes:

* "Availability", because a core is considered occupied by a parachain block candidate while that candidate is being made available. But cores mediate access to the entire parablock validation pipeline, not just availability.
* "Core", because many candidates can be made available in parallel, mimicking the parallel computation per core in a computer processor.

***

### Availability

Though cores gate the entire parachain block pipeline,\
the availability process alone determines when these cores are considered occupied vs free.

To recap, the goals of availability are:

1. To ensure that approvers will always be able to recover the PoVs to validate their assigned blocks
2. To ensure that parachain nodes can recover blocks in the case that a parablock author fails to share them, through malintent or malfunction

***

### Core States

Free

![](img/free.png)

Scheduled

![](img/scheduled.png)

Occupied

![](img/occupied.png)

Notes:

* Before going any farther we need to talk about core states
* CoreState: Free -> core has not been assigned a parachain via lease or on-demand claim
* CoreState: Scheduled -> Core has an assigned parachain and is currently unoccupied
* CoreState: Occupied -> Core has assignment and is occupied by a parablock pending availability

***

### The Availability Process

1. Block author places a candidate on-chain as backed, immediately occupying its scheduled core
2. Candidate backers distribute erasure coded PoV chunks
3. Validators distribute statements as to which candidates they have chunks for
4. Availability threshold is met (2/3 vs the 1/3 needed to reconstruct POV)
5. Candidate marked as included on chain and core freed
6. Approvers or parachain nodes retrieve PoV chunks as needed

***

### Cores and Blockspace Over Time

![](img/Train.jpeg)

Notes:

Metaphor:

* Relay chain: Train loading bay
* Relay block: Train leaving station every 6 seconds
* Parachain block: One train car worth of cargo
* Availability core: Car index within all trains

If you have a lease on core 4, then you have the right to fill train car 4 on each train with whatever you want to ship.

Q: How would an on-demand claim be represented in this metaphor?

***

## Mapping Leases and Claims to Validator Subsets

***

### The Big Picture

![](img/cores_big_picture.svg)

Notes:

* Which steps of the parachains protocol are missing, and why?
* Going to dive into each piece
* Questions?

***

### Assigning Leases and Claims to Cores

![](img/pairing_leases_and_claims_with_cores.svg)

Notes:

* Leases have indices and pair to cores with the same index
* Cores not designated as on-demand and without a paired lease are left free, their blockspace wasted
* When on-demand claims are queued, they are each assigned a designated core in ascending order, looping when reaching the last core

***

### Assigning Backing Groups to Cores

![](img/pairing_backing_groups_with_cores.svg)

Notes:

* Round robin, fixed intervals

This prevents a byzantine backing group from interrupting the liveness of any one parachain for too long.

***

### Backing Group Formation

![](../execution-sharding/img/validator-groups.png)

Notes:

* Validators randomly assigned to groups at start of session.
* Group count is active validator count / max group size rounded up
* Groups are partitioned such that the largest group and smallest group have a size difference of 1

***

![](img/dice.jpeg)

### Assigning Approvers to Cores

* Randomness via schnorrkel::vrf
* Approver assignments activated with delay tranches until threshold met
* Results in 30-40 approvers checking each block
* Different assignments each block prevent DOS

***

### Putting the Pieces Together

![](img/cores_big_picture.svg)

***

### Occupying Assigned Cores: With Lease

![](img/occupying_assigned_cores_with_lease.svg)

Notes:

Q: What step of the parachains protocol takes place between "Supplied backable candidate" and "availability process?

***

### Occupying Assigned Cores: On Demand

![](img/occupying_assigned_cores_on_demand.svg)

***

### Core States in the Runtime

In file: polkadot/runtime/parachains/src/scheduler.rs

```rust[1|3-8|5,10-16]
pub(crate) type AvailabilityCores<T> = StorageValue<_, Vec<Option<CoreOccupied>>, ValueQuery>;

pub enum CoreOccupied {
    /// A parathread (on-demand parachain).
    Parathread(ParathreadEntry),
    /// A lease holding parachain.
    Parachain,
}

/// Parathread = on-demand parachain
pub struct ParathreadEntry {
	/// The claim.
	pub claim: ParathreadClaim,
	/// Number of retries.
	pub retries: u32,
}
```

Notes:

Q: When Option is None, what does that indicate?

* Which para occupies a core is stored separately in the following structure

***

### Core Assignments in The Runtime

In file: polkadot/runtime/parachains/src/scheduler.rs

```rust[1|3-10|9,12-17]
pub(crate) type Scheduled<T> = StorageValue<_, Vec<CoreAssignment>, ValueQuery>;

pub struct CoreAssignment {
    /// The core that is assigned.
    pub core: CoreIndex,
    /// The unique ID of the para that is assigned to the core.
    pub para_id: ParaId,
    /// The kind of the assignment.
    pub kind: AssignmentKind,
}

pub enum AssignmentKind {
	/// A parachain.
	Parachain,
	/// A parathread (on-demand parachain).
	Parathread(CollatorId, u32),
}
```

Notes:

* Vec of all core assignments
* Pairs ParaId with CoreIndex
* AssignmentKind carries retry info for on-demand

***

### How Cores Gate Each Step of the Parachains Protocol

***

### How Core Assignments Mediate Backing

Each parablock candidate is built in the context of a particular `relay_parent`.

Validators query their core assignment as of `relay_parent` and refuse to second candidates not associated with their backing group.

Notes:

* Relay parent context: max PoV size, current parachain runtime code, and backing group assignments.

***

#### How Core Assignments Mediate Backing (Cont.)

`handle_second_message()` in the Backing Subsystem.

```rust[1|6]
if Some(candidate.descriptor().para_id) != rp_state.assignment {
	gum::debug!(
		target: LOG_TARGET,
		our_assignment = ?rp_state.assignment,
		collation = ?candidate.descriptor().para_id,
		"Subsystem asked to second for para outside of our assignment",
	);

	return Ok(())
}
```

***

### Cores and Backing On-Chain

* For each core that is either unoccupied or is about to be a new candidate is found
* A candidate for the parachain scheduled next on that core is provided to the block author
* Backed on-chain -> immediately occupies core

Notes:

* Review possible core states
* Mention time-out vs made available

Q: What does "immediately occupies core" imply?

***

### Cores and Backing On-Chain, Code

Code determining whether to back a candidate and which, greatly simplified

```rust[1|24|2-4|5-13|13-23|28-29]
	let (para_id) = match core {
		CoreState::Scheduled(scheduled_core) => {
			scheduled_core.para_id
		},
		CoreState::Occupied(occupied_core) => {
			if current_occupant_made_available(core_idx, &occupied_core.availability)
			{
				if let Some(ref scheduled_core) = occupied_core.next_up_on_available {
					scheduled_core.para_id
				} else {
					continue
				}
			} else {
				if occupied_core.time_out_at != current_block {
					continue
				}
				if let Some(ref scheduled_core) = occupied_core.next_up_on_time_out {
					scheduled_core.para_id
				} else {
					continue
				}
			}
		},
		CoreState::Free => continue,
	};

	let candidate_hash =
		get_backable_candidate(relay_parent, para_id, required_path, sender).await?;
```

Notes:

* Discuss core freeing criteria
* `bitfields_indicate_availability`
  * next\_up\_on\_available
* availability time out
  * next\_up\_on\_timeout

***

### Cores and Approvals, Disputes, Finality

Each included candidate has already occupied an availability core

Approvals, Disputes, and Finality are only provided to included candidates

***

### Advantages Cores Give us Now

1. Predictability of parachain execution
2. Predictability of allocation for execution sharding

![](img/advantage.png)

Notes:

* Regularly rotating pairings between cores and backing groups lessen the impact of potential bad validator subsets
* Cores accommodate advance allocation making costs for parachains predictable
* Core time can be resold or split for precise allocation

***

## Cores and Roadmap Items

![](img/road.jpeg)

***

### Exotic core scheduling

* Multiple cores per parachain
* Overlapping leases of many lengths
* Lease + On-demand

![](img/exotic_core_scheduling.svg)

Notes:

* Each color represents a parachain\
  Metaphor:
* Multiple cars on the same train
* Overlapping time spans of rights to fill different train cars
* Long term rights to one car and buy rights to others for just one train

***

### Divisible and Marketable Blockspace

We want Parachains to buy, sell, and split blockspace such that they are allocated exactly as much as fits their needs.\
\


* Core sharing via use-threshold blockspace regions
* Secondary markets for blockspace regions

Notes:

* Example: Region spanning 100 blocks. Split the region use so that each of two parties can submit up to 50 parablocks. Ownership proportion is enforced throughout the region such that each party can't submit more than 5 out of the first 10 blocks.

***

### Framing Shift: Blockspace vs Core Time

Blockspace is a universal term for the product of blockchains, while core time is Polkadot's particular abstraction for allocating blockspace or other computation.

Cores can secure computation other than blocks. For example, a smart contract could be deployed on a core directly.

Allocating cores by time rather than for a fixed block size could allow for smaller or larger parachain blocks to be handled seamlessly.

***

### Resources

1. [Implementers Guide: Scheduler Pallet](https://paritytech.github.io/polkadot/book/runtime/scheduler.html)
2. [RFC: Agile Coretime](https://github.com/polkadot-fellows/RFCs/pull/1)
3. [RFC: Coretime Scheduling Regions](https://github.com/polkadot-fellows/rfcs/pull/3)
4. [Rob Habermeier's Blog: Polkadot Blockspace Over Blockchains](https://www.rob.tech/polkadot-blockspace-over-blockchains/)

***

## Questions
