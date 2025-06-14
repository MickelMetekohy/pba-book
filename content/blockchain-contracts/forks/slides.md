---
title: Blockchain Forks
duration: 60 minutes
description: Detailed Classification for Blockchain Forks Types
---

# Blockchain Forks

## Blockchain Forks

***

## Landscape

\---v

### Landscape

**Ideal World**

In an ideal world blockchains would look like this:\
\


![](img/no_fork.drawio.svg)

\---v

### Landscape

**Real World**

Things don't always go according to plan:

\
![](img/fork_small.drawio.svg)

\---v

### Landscape

**Chaotic Real World**

And sometimes they get extra messy:

\
![](img/fork_chaos.drawio.svg)

***

## What's the goal?

\---v

### What's the goal?

_**Fork Identification**_

![](img/forks_and_boxes.drawio.svg)

Notes:

There are different forks, they can have different shapes and reasons.\
We'll try to identify some examples.

\---v

### What's the goal?

_**Fork Categorization**_

![](img/forks_in_boxes.drawio.svg)

Notes:

Why?\
Forks in the same category will exhibit similar behavior and will require similar handling.\
Then when making changes we can easily figure out to which box the change belongs and react accordingly.

It's also worth pointing out that the whole web3 space is still very young and we are still figuring out how to name things appropriately.\
There is definitely still a lot of confusion about the fork types and the convention I will be using here today is based on the naming proposed by the MIT Digital Currencies Initiative.\
It will cover most of the common terms and hopefully will not be as self-contradictory as some of the terms used within the community.

\---v

### What's the goal?

_**Fork Confusion**_

\
BABE (sometimes):\
\
![](img/transitory_fork_unresolved.drawio.svg)

Notes:

To demonstrate the confusion think of BABE.\
BABE can have multiple block authors create blocks at the same time and then the chain forks.\
What type of a fork is it?\
Some of you might have heard about soft forks and hard forks, any idea which one it is?

***

## Fork Categorization

\---v

### Fork Categorization

_**Forks Family Tree**_

\
![](img/fork_family.drawio.svg)

Notes:

This is the core categorization of forks we'll be waking you through today.\
You don't need to understand the whole tree as we'll be going step by step.\
For now let's actually go back to the example from BABE and let's place it on the map.

***

## Transitory Forks

Notes:

For that we'll talk about transitory forks.

\---v

### Fork Categorization

_**Transitory Forks**_

\
![](img/fork_family_transitory.drawio.svg)

Notes:

One of the simplest forks that is rarely talked about so the name might not sound familiar.\
They are often also called short-lived forks or temporary forks.

\---v

### Transitory Forks

\
![](img/transitory_forks.drawio.svg)

Notes:

They usually arise from the fundamental protocol uncertainty or networking lag, but luckily they are usually resolved quickly by the network itself.\
For instance in BABE even if all the nodes are running the same software those forks can still happen when two nodes roll low enough numbers.\
In Bitcoin two miners might mine a block at roughly the same time.\
Over time one of the blocks wins due to some heuristics like the longest chain.\
Those forks are generally not a problem and only live on short timescales.

***

## Consensus Forks

Notes:

So now let's move to something more interesting.\
Consensus forks.

\---v

### Fork Categorization

_**Consensus Forks**_

\
![](img/fork_family_consensus.drawio.svg)

Notes:

Usually when you hear about forks you hear about those guys.\
They are the other branch and they also come in many flavours we'll discuss in a minute.

\---v

## Consensus Forks

### _Validity Set_

Notes:

But first before we understand the intricacies of consensus forks we need to understand the concept of the validity set and how it connects to the protocol.

\---v

### Consensus Forks

_**Validity Set**_

\
![](img/BTC_block.drawio.svg)

Notes:

It's best to see it through an example so let's look at the BTC block.\
You don't need to understand all the fields that are in it but for now take a look at the blocksize field as well as the block header itself.

_**Validity Set**_

\
![](img/BTC_header.drawio.svg)

\---v

### Consensus Forks

_**Validity Set**_

\
![](img/BTC_header_constraints.drawio.svg)

\---v

### Consensus Forks

_**Validity Set**_

\
![](img/validity_set.drawio.svg)

Notes:

So the validity set is a set of all hypothetical blocks that could be produced by the protocol.\
It's a set of all valid blocks under those rules.

So if there is a block D that for instance is too big, it's blocksize is bigger than the allowed one...

\---v

### Consensus Forks

_**Validity Set**_

\
![](img/universal_set.drawio.svg)

Notes:

Then it falls out of the validity set into the universal set of all possible data blobs.\
Only some of those data blobs are valid blocks.

\---v

### Consensus Forks

_**Validity Set**_

\
![](img/validity_set_old.drawio.svg)

Notes:

Let's actually look at an example.\
Imagine this is Bitcoins validity set and here we see a few blocks from it.\
The numbers at the top are initial few digits from the hashes representing those blocks.

Imagine all the Bitcoin nodes suddenly decide they really dislike when the first hash digit is odd.\
They only like when it's even so they band together and change the protocol to only accept hashes with an even first digit.

\---v

### Consensus Forks

_**Validity Set**_

\
![](img/validity_set_new.drawio.svg)

Notes:

This change in the protocol would reduce the validity set.\
It would be more constrained then before.\
Some of the previously valid blocks would no longer be valid under the new rules.\
What happens in that case?\
Can we predict that?

\---v

### Consensus Forks

_**Validity Set**_

![](img/validity_set_new.drawio.svg)![](img/venn_soft.drawio.svg)N ⊆ O

Notes:

To generally represent the same idea we'll be using the simpler representation on the right.\
Where the new set N is contained within the old set O.\
The fancy notion at the bottom says the same N is contained in O.

***

## Soft Forks

To understand the example from a second ago we'll dive into soft forks.

\---v

### Fork Categorization

_**Soft Forks**_

\
![](img/fork_family_soft.drawio.svg)

Notes:

Firstly soft forks are a type of a consensus fork and they are results of a change in the protocol and thus the validity set.

\---v

### Fork Categorization

_**Soft Forks**_

![](img/venn_soft.drawio.svg)N ⊆ O

* Backwards Compatible
* By making the consensus rules more restrictive the set of valid blocks gets smaller.
* Not every (and often none) of the blocks produced under old rules will get accepted by new nodes.

Notes:

So based on the venn diagram we have on the side we can see that the new consensus rules are more restrictive as the validity set shrinks.

New nodes produce blocks that are always accepted by old nodes.\
Old nodes generally don't produce blocks accepted by the new nodes.

Before we jump into demonstration is decreasing or increasing blocksize a soft fork?

\---v

### Fork Categorization

_**Soft Forks**_

![](img/venn_soft.drawio.svg)N ⊆ O**Examples:**\
\


* Decreasing blocksize
* Accepting only even/odd hashes
* Disallowing some transaction types

Notes:

Decreasing the block size restricts how many different blocks can be constructed so it makes the set smaller.\
It is a soft fork.\
The example we had a moment ago with the even hashes is also a soft fork as it adds another constraint on the previous protocol rules restricting them even further.\
Another good example would be banning some transaction types from use.

Now let's take a look at how forks work in practice and how they vary based on the hash power or staking power in favour of the protocol change.

\---v

### Fork Categorization

_**Soft Forks**_

![](img/venn_soft.drawio.svg)N ⊆ O![](img/soft_forks_s50.drawio.svg)

Notes:

So in this scenario we'll be looking at what happens if nodes with less than 50% hash power or stake want to soft fork.\
Remember that soft forking is simply making the consensus stricter.

In that case the blocks produced by new nodes are marked with N and they are accepted by the old chain but the old chain mines faster so they don't care about the new nodes.\
Blocks produced by old nodes are NOT accepted by the new nodes so the longest chain for new nodes is the short chain with only the N blocks.\
This is effectively a permanent fork.

\---v

### Fork Categorization

_**Soft Forks**_

![](img/venn_soft.drawio.svg)N ⊆ O![](img/soft_forks_g50.drawio.svg)

Notes:

In the similar example when the new nodes control more than 50% power the situation changes drastically.\
The new nodes mine faster and are the longest chain.\
But remember that old nodes accept the new blocks so if they new nodes mine faster the old nodes blocks get constantly reorged out.\
They are forced to update the software if they want their blocks to get accepted at all otherwise they loose all the rewards.

***

## Hidden Forks

Notes:

Now let's take a look at something a bit less known.\
Hidden forks.

\---v

### Fork Categorization

_**Hidden Forks**_

\
![](img/fork_family_hidden.drawio.svg)

Notes:

An edge case of soft forks.

\---v

### Fork Categorization

_**Hidden Forks**_

![](img/venn_hidden.drawio.svg)N ⊆ O

* Conflict-less
* The old, now excluded blocks were allowed but never used in practice.
* New nodes are theoretically stricter but practically accept all old blocks.
* Old nodes accept new blocks.

Notes:

So the venn diagram is exactly the same as in the normal soft fork case.\
But imagine that the the orange crescent, this is the part we're excluding from the old protocol when shifting to the new one... was never actually used.\
So for instance the block had an empty field that could have some arbitrary data inside, but everyone left it empty and never checked what was inside.\
The new protocol puts something meaningful in the empty field but doesn't require it.\
Because old nodes never used this field pretty much all old blocks will be accepted under the new rules.

TL;DR the stuff we removed from the validity set wasn't even used despite being technically valid.

\---v

### Fork Categorization

_**Hidden Forks**_

![](img/venn_hidden.drawio.svg)N ⊆ O**Examples:**\
\


* Assigning non-conflicting uses to empty opcodes.
* BTC Ordinals using empty opcodes to implement BTC NFTs.

Notes:

A good example of that assigning new optional use-cases for previously unused opcodes as with the example of the recent Bitcoin Ordinals update.

\---v

### Fork Categorization

_**Hidden Forks**_

![](img/venn_hidden.drawio.svg)N ⊆ O![](img/soft_forks_hidden.drawio.svg)

Notes:

And the reason why they are hidden... is they are not even manifesting as forks despite the consensus change.\
All nodes effectively accept each others blocks so there is no conflict.

***

## Hard Forks

Notes:

\---v

### Fork Categorization

_**Hard Forks**_

\
![](img/fork_family_hard.drawio.svg)

\---v

### Fork Categorization

_**Hard Forks**_

![](img/venn_hard.drawio.svg)O ⊆ N

* Forwards Compatible
* By making the consensus rules less restrictive the set of valid blocks gets bigger.
* Not every (and often none) of the blocks produced under new rules will be accepted by the old nodes.
* Every block produced under old rules will get accepted by new nodes.

\---v

### Fork Categorization

_**Hard Forks**_

![](img/venn_hard.drawio.svg)O ⊆ N**Examples:**\
\


* Increasing blocksize
* BTC Cash fork at first\*
* Adding new transaction types
* Increasing max nonce value

\---v

### Fork Categorization

_**Hard Forks**_

![](img/venn_hard.drawio.svg)O ⊆ N![](img/hard_forks_s50.drawio.svg)

Notes:

First let's go through the scenario of a hard fork with less than 50% support.\
Remember that the rules were loosened this time.\
If new guys accept old blocks so because they have less than 50% power they get constantly reorged out.\
There is no permanent fork in this scenario and the change will not go through if if it has this limited support.

\---v

### Fork Categorization

_**Hard Forks**_

![](img/venn_hard.drawio.svg)O ⊆ N![](img/hard_forks_g50.drawio.svg)

Notes:

In the case of more than 50% support the new guys miner faster but they are no accepted by the old nodes so they go ahead.\
Old nodes maintain the old chain and the community is split.\
So if there is a major change that most people accept but not everyone it will always fork the chain.

***

### Small Summary

![](img/soft_forks_s50.drawio.svg)\
![](img/soft_forks_g50.drawio.svg)![](img/hard_forks_s50.drawio.svg)\
![](img/hard_forks_g50.drawio.svg)

Notes:

Now that we've seen both soft and hard forks...\
If we'd manually increase the difficulty of mining in the BTC network would that be a soft or hard fork?\
Hard.

Also let's reiterate.\
We only have permanent forks in soft forks with under 50% support and in hard forks with over 50% support.

***

## Full Forks

\---v

### Fork Categorization

_**Full Forks**_

\
![](img/fork_family_full.drawio.svg)

\---v

### Fork Categorization

_**Full Forks**_

![](img/venn_full.drawio.svg)O ∩ N = ∅

* Fully Incompatible
* Soft + Hard
* By changing the consensus rules the sets can become disjoint or overlapping.
* Most (and often all) blocks produced under one ruleset are not accepted under the other.

\---v

### Fork Categorization

_**Full Forks**_

![](img/venn_full.drawio.svg)O ∩ N = ∅**Examples:**\
\


* Changing the hashing function
* Changing the signature scheme
* Specific combinations of soft and hard forks
* BTC Cash fork in the end\*

\---v

### Fork Categorization

_**Full Forks**_

![](img/venn_full.drawio.svg)O ∩ N = ∅![](img/full_forks__&_50.drawio.svg)

***

### Summary

![](img/soft_forks_s50.drawio.svg)\
![](img/soft_forks_g50.drawio.svg)![](img/hard_forks_s50.drawio.svg)\
![](img/hard_forks_g50.drawio.svg)![](img/full_forks__&_50.drawio.svg)

Notes:

* Bitcoin cash pivot from hard to full because they didn't have enough HP.
* Soft are often preferred for changes because with >50%HP they do not fracture the community (BTC community logic)
* Hard can be preferred as they seem to better represent minorities.\
  If some people don't agree with the majority they naturally fork off and are not peer pressured to follow (ETH community logic)

***

## Thank you!

***

![](img/forks.drawio.svg)
