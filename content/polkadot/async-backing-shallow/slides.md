---
title: Shallow Dive, Asynchronous Backing
duration: 30 min
description: >-
  Decoupling Backing and Inclusion Through Advance Work Based on Happy Path
  Assumptions
---

# Shallow Dive, Asynchronous Backing

Notes:

Hello again everyone

Today I'll be speaking to you about asynchronous backing, the new feature which delivers shorter parachain block times and an order of magnitude increase in quantity of Polkadot blockspace.

Lets get to it

***

## Overview

* Synchronous vs asynchronous
* Why is asynchronous backing desirable?
* High level mechanisms of async backing
* The unincluded segment, and prospective parachains
* Async backing enabling other roadmap items

***

## Synchronous Backing Simplified

![](img/synchronous_backing_simplified.svg)

Notes:

* The dividing line between the left and right is when a candidate is backed on chain
* Approvals, disputes, and finality don't immediately gate the production of farther candidates.\
  So we don't need to represent those steps in this model.

***

## Async Backing Simplified

![](img/async_backing_simplified_1.svg)![](img/async_backing_simplified_2.svg)![](img/async_backing_simplified_3.svg)

Notes:

Our cache of parablock candidates allows us to pause just before that dividing line, on-chain backing

***

## The Async Backing Optimistic Collator Assumptions

1. "The best existing parablock I'm aware of will eventually be included in the relay chain."
2. "There won't be a chain reversion impacting that best parablock."

\
\


> The Stakes Are Low

Notes:

Best is determined by a process similar to the BABE fork choice rule.\
Brief BABE fork choice rule review

***

## Advantages of Asynchronous Backing

1. 3-5x more extrinsics per block
2. Shorter parachain block times 6s vs 12s
3. Resulting 6-10x boost in quantity of blockspace
4. Fewer wasted parachain blocks

Notes:

1. Collators have more time to fill each block
2. Advance work ensures backable candidates for each parachain are present to be backed on the relay chain every 6 seconds
3. Self explanatory
4. Allow parachain blocks to be ‘reused’ when they don’t make it onto the relay chain in the first attempt

***

## Parablock Validation Pipelining

![](img/async_backing_pipelining.svg)

***

## Synchronous Backing, Another Look

![](img/synchronous_backing_1.svg)![](img/synchronous_backing_2.svg)![](img/synchronous_backing_3.svg)

Notes:

Image version 1:

* Now let's take a closer look at when each step of backing and inclusion takes place both with synchronous and asynchronous backing.

Image version 3:

* Whole process is a cycle of duration 12 seconds (2 relay blocks).
* No part of this cycle can be started for a second candidate of the same parachain until the first is included.

***

## Async Backing, Another Look

![](img/async_backing_1.svg)![](img/async_backing_2.svg)![](img/async_backing_3.svg)

Note:

Image version 1:

* Candidates stored in prospective parachains (detail on that later)

Image version 2:

* Now we see our relay block cycle.
* It is 6 seconds rather than 12.
* It completes on-chain backing for one candidate and inclusion for another each cycle.

Image version 3:

* Collation generation and off-chain backing are outside of the relay block cycle.
* Because of this, collators have the freedom to work several blocks in advance. In practice, even working 2-3 blocks in advance gives a collator ample time to fully fill blocks (PoV size 5MiB)
* Notice that a part of the collation generation context, the unincluded segment, comes from the collator itself.

***

## The Unincluded Segment

* A parachain's record of all parablocks on a particular chain fork produced but not yet included
* Used to apply limitations when constructing future blocks
* Lives in the parachain runtime
* Viewed from the perspective of a new parablock under construction

Notes:

Limitation example, upward messages remaining before the relay chain would have to drop incoming messages from our parachain

***

## Unincluded Segment

![](img/unincluded_segment_1.svg)

Notes:

* Segment added to as each new block is imported into the parachain runtime
* Segment shrinks when one of its ancestor blocks becomes included
* Maximum unincluded segment capacity is set both on the parachain and relay chain

***

## Unincluded Segment

![](img/unincluded_segment_2.svg)

Notes:

UsedBandwidth:

* pub ump\_msg\_count: u32,
* pub ump\_total\_bytes: u32,
* pub hrmp\_outgoing: BTreeMap\<ParaId, HrmpChannelUpdate>,

***

## Prospective Parachains

* The relay chain's record of all candidates on all chain forks from all parachains
* As if you folded all unincluded segments into one huge structure
* Used to store candidates and later provide them to the on-chain backing process
* Lives in the relay client (off chain)

***

## Prospective Parachains Snapshot

![](img/Prospective_Parachains_Overview.svg)

Notes:

* Fragment trees only built for active leaves
* Fragment trees built per scheduled parachain at each leaf
* Fragment trees may have 0 or more fragments representing potential parablocks making up possible futures for a parachain's state.
* Collation generation, passing, and seconding work has already been completed for each fragment.

***

## Async Backing Simplified

![](img/async_backing_simplified_3.svg)

Notes:

Returning to our most basic diagram

* Q: Which structure did I leave out the name of for simplicity, and where should that name go in our diagram?
* Q: Which did I omit entirely?

***

## Async Backing and Exotic Core Scheduling

![](img/exotic_scheduling.svg)

Notes:

* What is exotic core scheduling?
  * Multiple cores per parachain
  * Overlapping leases of many lengths
  * Lease + On-demand
* How does asynchronous backing help?
* The unincluded segment is necessary to build 2 or more parablocks in a single relay block

***

## Resources

1. [Polkadot Async Backing PR](https://github.com/paritytech/polkadot/pull/5022)
2. [Cumulus Async Backing PR](https://github.com/paritytech/cumulus/pull/2300)
3. [Implementers Guide: Prospective Parachains](https://github.com/paritytech/polkadot/blob/631b66d5daa642fad7ed0a9712194c5b85b96563/roadmap/implementers-guide/src/node/backing/prospective-parachains.md)

***

## Questions
