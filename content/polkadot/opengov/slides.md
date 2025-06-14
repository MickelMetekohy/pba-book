---
title: OpenGov
duration: 1 hour
description: The Polkadot ecosystem on-chain governance solution
---

# OpenGov

Notes:

Hello!

I'm Bradley Olson

Was student at first Academy in Cambridge

Currently on Parachains Core Team at Parity

Making Polkadot truly decentralized requires a robust, agile, and democratic system of governance.

Gavin has put a lot of effort over the last year or so into crafting a system which does those words justice, OpenGov.

I'm here to give you an overview of what OpenGov is and to surface some new information about how it is performing on Kusama.

So lets get to it

***

## Overview

* Why blockchain governance?
* Why on-chain?
* Goals of on-chain governance
* Initial Solution, Governance V1
* Improvement, OpenGov
* How is it going? By the numbers.
* OpenGov and you

***

## Reasons for Blockchain Governance

* Software as executive branch
  * Applies existing laws (code) in pre-defined ways
  * Protocol security ensures the letter of those laws is followed
* But evolving protocols need a legislative branch
  * To update the laws (code)
  * To rectify cases where letter != spirit (bugs)
  * To trigger parts of the system that aren't on a set schedule
  * To spend treasury funds
* Legeslative can be on or off chain

***

## Why On-chain?

* Off-chain governance
  * Formal proposal by dev team
  * Discussions, debates, and media campaigns
  * Hard fork
* Issues
  * Centralization
  * Low throughput
  * Long decision period
  * Little accessibility

![](img/Bitcoin.png)![](img/Ethereum.png)

***

## Goals of On-chain Governance

* **Transparency**: Decisions by who and by what rules?
* **Decentralization**: Distributed power, weighted only by commitment and conviction
* **Security**: Harmful proposals don't pass or have limited scope
* **Accessibility**: Easy to draft proposal, to receive vote, to vote yourself, and to vote by proxy
* **Concurrency**: Maximize simultaneous referenda as security allows
* **Speed**: Each referendum completed as fast as security allows
* **Agility**: Speed is responsive to support/controversy

***

## Governance V1

![](img/Polkadot.png)

* Tri-cameral system: Referenda, council, and technical committee
* Single track
* 1 referendum at a time
* Root origin (Unlimited Power!)
* 28 day referendum
* 1 month minimum enactment period
* Emergency handled technical committee
* Cancellations by council and technical committee
* Most proposals initiated by council
* Fully council controlled roles such as tipping

***

## Gov V1, Room for Improvement

The good:

* Security
* Transparency

The bad:

* Decentralization
* Concurrency
* Speed
* Agility

![](img/Snail.jpeg)

***

## OpenGov Overview

* Origins and tracks
* Lifecycle of a referendum
* Support and approval threshold curves
* The Polkadot Fellowship
* Vote delegation by track
* OpenGov and governance goals

![](img/overview.png)

***

## Origins

* Level of privilege that code executes with
* Similar to user on Unix
* Proposal is two things
  * Operation: What should happen
  * Origin: Who authorizes it
* Many operations require a specific origin

***

![](img/rail_road_tracks.jpeg)

## Origins and Tracks

* Each origin is served by a referendum track
* A track can serve more than one origin
* These tracks are totally independent from one another
* Track examples: Root, ParachainAdmin, BigSpender, Tipper
* Emergency tracks: ReferendumCanceler, ReferendumKiller

***

## Track Parameters

Parameters give us the ability to find an optimal balance between security and throughput.

The security needs of the Tipper track are very different than those of the Root track.

* Lead-in period duration
* Decision period duration
* Confirmation period duration
* Minimum enactment period
* Concurrency, how many referenda can run in this track at a time
* Support and Approval threshold curves

***

#### OpenGov Tracks

![](img/TracksTable.webp)

Notes:

Highlight difference between parameters of WhiteListedCaller and Root tracks

***

## Criteria for Passing a Proposal

* Approval: Approving votes/total votes cast, weighted by conviction
  * Conviction: Locking tokens for longer periods scales their voting impact up to a maximum of 6x with a lockup duration of 896 days
* Support: Approving votes/total possible vote pool, disregarding conviction

***

## Decision and Confirmation Periods

* If Approval and Support thresholds met, confirmation period begins
* Approval and Support must remain above respective thresholds for entire confirmation period
* Confirmation period concludes -> proposal approved early
* Decision period expires -> proposal rejected
* There is only one decision period, during which a proposal can potentially enter and leave many confirmation periods if thresholds aren't consistently met

***

## Lifecycle of A Referendum

![](img/lifecycle_of_a_referendum.png)

Notes:

Steps in order: **Proposing, Lead In, Deciding, Confirming, Enactment**

***

## Support and Approval Threshold Curves

* We want agility
  * Well supported proposals pass quickly
  * Controversial proposals get more deliberation
* Addressed with time varying curves
  * Support threshold
    * Starts at \~50%
    * Ends at minimum secure turnout for track\
      (EX: Big Spender ends at 0 + epsilon %)
  * Approval threshold
    * Starts at 100%
    * Ends at 50 + epsilon %
* Monotonically decreasing at rates determined by track specific security needs

***

### Example Support and Approval Curves

![](img/support_and_approval_curves.png)

Notes:

From PolkaWorld Article in Resources

***

### Vote Delegation

* Traditional delegation: You entrust one third party with your vote on all matters
* Delegation by track: You may delegate your vote to one or more third parties on a per track basis
* EX: Tipper vote delegated to local ambassador, WhiteListedCaller vote delegated to Parity Technologies, vote retained for all other tracks
* This is likely a first!

![](img/vote.jpeg)

***

![](../async-backing-deep/img/stopwatch.png)

### OpenGov Acting Under Pressure

Typical path to safety: Lower throughput and restricted origins

But in emergencies we may need to pass proposals that both require root origin and are time critical!

Solution: Some sort of oracle capable of providing expert information

***

### Oraclization of Expert Information

1. Track everyone's level of expertise
2. Allow experts to register sentiment
3. Aggregate opinions by level of expertise

> But how are these steps accomplished?

***

### Enter...  The Polkadot Fellowship

***

Purely on-chain membership body to recognize and compensate all individuals who hold and use expert knowledge of Polkadot in line with its broad interest and philosophy

Members hold rank denoting proven level of expertise and commitment as recognized by their peers and, for higher ranks, through general referendum.

***

### Who Make up the Fellowship?

* Experts in the Polkadot core protocol who maintain a consistent level of active contribution
* Notably this does not include core developers of independent parachain protocols, which should develop their own protocol specific fellowships as needed.
* Trajectory
  * Currently: < 100 core developers, mostly from Parity or the Web3 Foundation
  * Next year or two: Hundreds
  * Ideal far future: Tens of thousands, independent of any centralized entity
* Only one fellowship for Polkadot and Kusama

***

### Function of the Fellowship

* WhiteListedCaller track
  * Root privileges
  * More agile
  * Maintains reasonable safety via Fellowship
* White list proposals must pass two votes
  * Expertise weighted Fellowship vote via second referendum pallet instantiation
  * Same general referendum as other tracks, still requiring majority vote from DOT holders
* Just an oracle!
* Secondarily intended to cultivate a long term base of Polkadot core developers outside of Parity

Notes:

Stress that as an oracle, the Fellowship can't take any action on its own. Any white listed call will still require substantial DOT-holder backing.

***

### OpenGov and Governance Goals

* Open source + single process + track abstraction -> Transparency
* Liberal proposal creation + greater throughput + per-track delegation -> Accessibility
* Accessibility + No special bodies -> Decentralization
* Limited origins + emergency tracks + white list -> Security
* Multiple tracks + low risk tracks -> Concurrency
* Low risk tracks + early confirmation -> Speed
* Support and approval threshold curves + white list -> Agility

***

OpenGov\
\
By The Numbers
--------------

***

### Governance Activity

![](img/proposals_per_day.png)

> 5.5x more daily governance activity

***

### Proposal Origins

![](img/proposals_from_democracy.png)

> Proposals now primarily authored via democracy

***

### Treasury Usage

![](img/treasury_waste_since_opengov.png)

> Treasury funds used more efficiently

***

### OpenGov and You

* Participate in OpenGov and Polkadot Fellowship on Polkadot and Kusama
* Can customize OpenGov instances per parachain
* Custom fellowships per parachain
* Potentially create non-technical fellowships, such as a fellowship for brand ambassadors

***

### Resources

1. [PolkaWorld Hands-On OpenGov](https://polkaworld.medium.com/a-hands-on-guide-for-kusamas-open-gov-governance-system-98277629b0c5)
2. [OpenGov Article from Moonbeam Team](https://moonbeam.network/blog/opengov/)
3. [Gavin’s Polkadot Decoded 2022 talk](https://www.youtube.com/watch?v=EF93ZM_P_Oc)
4. [Gov (OpenGov and V1) tracking](https://polkadot.polkassembly.io/opengov)
5. [OpenGov tracking](https://kusama.subsquare.io/)

***

## Questions

***

### OpenGov in Action

* Vote - [https://kusama.subsquare.io/referenda](https://kusama.subsquare.io/referenda)
* Delegate vote - [https://kusama.subsquare.io/referenda](https://kusama.subsquare.io/referenda)
* Submit proposal - [https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkusama-rpc.dwellir.com#/referenda](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fkusama-rpc.dwellir.com#/referenda)
