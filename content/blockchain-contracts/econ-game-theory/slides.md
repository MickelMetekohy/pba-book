---
title: Econ & Game Theory in Blockchain
duration: 60 minutes
description: Blockchain applications of Econ & Game Theory
---

# Econ & Game Theory in Blockchain

## **Econ & Game Theory in Blockchain**

Notes:

* Presenter Introduction
* Timeline clarification (after mod 2 and 3)
* Today we'll be going through a brand new lecture on Econ & Game Theory in Blockchain

***

## What's the goal?

Notes:

What's the goal of this lecture?

\---v

### What's the goal?

![Econ Box Open](img/Econ_Box_Open.svg)

* Demand & Supply
* Markets
* Nash Equilibrium
* Schelling Point
* **...**

Notes:

By now you all should be familiar with all the terms and techniques from the Economy and Game Theory module like the Demand & Supply or Nash equilibrium.

\---v

### What's the goal?

![Econ Box](img/Econ_Box_Closed.svg)![Blockchain Box Open](img/Blockchain_Box_Open.svg)

* Consensus
* Protocol
* Tokens
* State Transition Functions
* **...**

Notes:

And you also just finished covering the basics of Blockchains so you all should be familiar with state transition functions as well as have some understanding of consensus protocols.

\---v

### What's the goal?

![Econ and Blockchain Handshake](img/Econ_Handshake_Blockchain.svg)

Notes:

Having all that in mind, the goal of this lecture is to combine the two and see how the economy and game theory can be applied to blockchain.\
To do that we'll provide some exemplary use-cases and case studies.

***

## Landscape

Notes:

But first let's start with a quick summary of how we'll be approaching to bridge the gap between the two modules.

\---v

### Landscape

* Systems as Games

![Game Pad](img/game.svg)

Notes:

Firstly, we'll be looking at various blockchain systems as isolated games.

\---v

### Landscape

* Systems as Games
* Nodes/Miners/Validators as Players

![Laptop user cheering](img/player.svg)

Notes:

Participants in those games will be for instance the miners, like in the Bitcoin protocol, maybe the validators in the Polkadot protocol or just some users of your smart contract.

\---v

### Landscape

* Systems as Games
* Nodes/Miners/Validators as Players
* Protocols as Game Rules

![Checklist with points](img/assumptions.drawio.svg)

Notes:

The protocol is essentially a set of rules that will define the game itself.\
The one we will be analyzing.

\---v

### Landscape

* Systems as Games
* Nodes/Miners/Validators as Players
* Protocols as Game Rules
* Cryptocurrencies as Points

![BTC symbol](img/bitcoin.svg)

Notes:

And to properly analyze those games we need to have some value representation, which in our case will be usually cryptocurrencies.

\---v

### Landscape

* Systems as Games
* Nodes/Miners/Validators as Players
* Protocols as Game Rules
* Cryptocurrencies as Points
* Rewards & Punishments as Incentives

![Gavel Hammer](img/gavel.svg)

Notes:

And finally we'll be having various reward and punishment schemes that will shape the incentives of the players.

Now that we have all the elements defining our blockchain games we can look for further parallels.

\---v

## Market Emergence

Notes:

And first let's take a look at something that hopefully very familiar: Markets

\---v

### Market Emergence

_"A market is a composition of systems, institutions, procedures, social relations or infrastructures whereby parties engage in exchange."_

Notes:

So a market is a composition of systems where ppl exchange stuff.\
This is the simplest way of putting it.

And Markets are the cornerstone of our economy and they are everywhere which also means they are thoroughly studied.\
Which is very fortunate for us.

Now let's look at something that might also be pretty familiar to many...

\---v

### Market Emergence

_**Fee Market**_

![Chart of Bitcoin fees over time](img/fees.png)

Notes:

The fee market.\
That's a chart of the average transaction fees in the Bitcoin network over time.\
As you can see the price is constantly fluctuating.

\---v

### Market Emergence

_**Fee Market**_

**Fees/Tips**

* Users bid with the fees
* Miners select highest fee transactions

![Scales Icon](img/scales.svg)

Notes:

Let's dive a bit deeper.\
So the users are bidding with how much they are willing to pay and miners are choosing the most lucrative transactions.\
If miners already included all the best transactions and there are not many new ones coming in they need to start accepting lower fees, so the price drops.\
But wait...?

\---v

### Market Emergence

_**Fee Market**_

**What is the product?** ![Blockspace in Polkadot](img/blockspace.drawio.png)

Notes:

What is the actual product being exchanged here? When you have the crude oil market the goods being exchanged are clearly defined.\
It's crude oil barrels.\
What is actually being traded in here?

Anyone has an idea what it might be?

\---v

### Market Emergence

_**Fee Market**_

**What is the product?**

* What is being exchanged is the blockspace
* Miners produce blockspace and effectively auction it to users

![Blockspace in Polkadot](img/blockspace.drawio.png)

Notes:

It's the BLOCKSPACE.\
Miners secure and produce blockspace and sell it in an auction to various users.\
Blockspace as a product is actually a pretty new way of thinking about blockchains so I highly suggest checking out the article linked in the notes.

* [https://www.polkadot.network/blog/blockspace-blockspace-ecosystems-how-polkadot-is-unlocking-the-full-potential-of-web3/](https://www.polkadot.network/blog/blockspace-blockspace-ecosystems-how-polkadot-is-unlocking-the-full-potential-of-web3/)

\---v

### Market Emergence

_**Fee Market**_

**Market Equilibrium**

* The transactions that manage to get into the blocks have fees representative of the current market equilibrium

![Chart showing a market equilibrium](img/market_eq.drawio.svg)

Notes:

The price of blockspace is determined by the market equilibrium of supply and demand.\
Demand force is the users willing to transact and supply is the miners producing the blockspace.\
Transactions that are actually included represent the current equilibrium.

\---v

### Market Emergence

_**Fee Market**_

**Supply & Demand**

* In extreme cases the demand can raise so much that the fees overwhelm the network

![Rising graph icon](img/rising.svg)

Notes:

We all know that the transaction fees can sometimes get outrageous.\
In cases where many users want to transact the demand can skyrocket.\
And what we see is the price equilibrium following suit.

\---v

### Market Emergence

_**Fee Market**_

**Supply & Demand**

* In extreme cases the demand can raise so much that the fees overwhelm the network
* Most economic markets can react to growing demand with increased supply, but that is not directly possible in most blockchains

![Stack of goods on a conveyor belt](img/goods.svg)

Notes:

And now let's think of what normal markets do.\
If our demand and price go extremely high the suppliers would have an incentive to produce more.\
But in blockchains that's not directly possible.\
More miners often don't mean more blockspace but MORE SECURE blockspace.\
That means a better quality blockspace.

So the supply is often fixed and the demand is fluctuating.\
This is often the cause for the very volatile fee market.

\---v

### Market Emergence

_**Fee Market**_

**Supply & Demand**

* In extreme cases the demand can raise so much that the fees overwhelm the network
* Most economic markets can react to growing demand with increased supply, but that is not directly possible in most blockchains

![CryptoKitties Logo](img/kitty.png)

Notes:

And according to that theory some large blockchains actually tried implementing variable size blocks to react to the demand, but it's a pretty complex task and a big tradeoff.

Some of you maybe recognize this image as the CryptoKitties game on Ethereum.\
It's a game where you can buy and breed digital cats.\
It was so popular that it actually clogged the Ethereum network and made normal transactions nearly unfeasible.\
And maybe now you have some additional insights into what actually happened there.

\=5 sec pause=

***

## Nash Equilibrium

Notes:

Now let's look at something a bit different that allows us to predict what users would do...\
a Nash Equilibrium.

\---v

### Nash Equilibrium

* Strategy from which no player wants to deviate
* But what's the strategy for BTC mining?

Notes:

Nash Equilibrium is strategy from which no player wants to deviate.\
Pretty simple but what's the strategy for BTC mining? How can we leverage that knowledge?

\---v

### Nash Equilibrium

![Honest Mining Meme](img/honest_mining_meme.jpg)

Notes:

And more importantly...\
being honestly is the answer, right?

\---v

### Nash Equilibrium

_**Bitcoin Mining**_

![Bitcoin Logo](img/bitcoin.svg)

Notes:

Let's dive in and actually see what's the answer.\
What's the Nash Equilibrium of Bitcoin mining? Is it being honest or dishonest?

\---v

### Nash Equilibrium

**Assumptions:**

* Only 2 miners
* Block reward = 2
* Difficulty scales with number of honest miners
* Miners are rational actors
* Dishonest miners do not cooperate

![Payoff Table](img/nash.drawio.svg)

Notes:

Here we have a few assumptions, but the main ones are:

* imagine we have only 2 miners
* the block rewards is 2
* miners can be honestly following the protocol or try to cheat and push invalid blocks (for instance one where they get 999 bitcoins)

Let's figure out how many bitcoins each one of them will mine on average.

\---v

### Nash Equilibrium

![Payoff Table](<img/nash.drawio (1).svg>)

Notes:

If both miners are not mining honestly, none of them produce valid bitcoin blocks...\
then there are no ACTUAL bitcoins being mined.\
Remember that they don't cooperate but for instance try and push blocks with 9999 BTC in their account.\
So the reward is 0 for both.

\---v

### Nash Equilibrium

![Payoff Table](<img/nash.drawio (2).svg>)

Notes:

If both are working honestly and making valid blocks they have an equal chance to mine a block and reap the rewards.\
Rest of the nodes will accept those blocks but the two miners compete for the same resource so each one will get a single BTC on average (as the mining reward is 2).

\---v

### Nash Equilibrium

![Payoff Table](<img/nash.drawio (3).svg>)

Notes:

If one of them is dishonest the other one can still keep working honestly and reap greater rewards as there is no competition.\
In that case the honest party gains 2 BTC.

Now that we know who earns how many bitcoins in each scenario we need to shift out attention to another important force.\
Things like Twitter, Facebook or Bitcoin are often deemed as valuable because of their Network Effect.

\---v

### Nash Equilibrium

\


_**Network Effect**_

_"The network effect is a business principle that illustrates the idea that when more people use a product or service,_\
_its value increases."_

Notes:

Generally the more ppl use some platform or believe in something the more valuable it is.\
It's a pretty simple concept but it's very important in the blockchain space.\
Bitcoin is precious to many because many people believe in it and mine it and exchange it.\
In blockchains if more people use your chain it's more valuable.

\---v

### Nash Equilibrium

\


_**Network Effect**_

\
**Assumptions revisited:**

* Only 2 miners
* Block reward = 2
* Difficulty scales linearly with number of honest miners
* Miners are rational actors
* Dishonest miners do not cooperate
*   Token price scales quadratically with the number of honest miners

    * 1 honest miner -> 1$
    * 2 honest miners -> 4$

    Notes:

    Let's add this extra assumption into our model.\
    If there are more miners securing the network the coins itself are more valuable.\
    We will use a super simple model here where the price of a coin is a square of the number of miners.\
    We will be investigating small systems so it is a good enough approximation.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (4).svg>)

    Notes:

    We can apply the changes by changing the evaluations of the miners coins.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (4b).svg>)

    Notes:

    If both miners honestly secure the network the coin price is 4 and in case of single honest miner the price is 1.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (5).svg>)

    Notes:

    Now we can actually focus on finding the Nash Equilibrium\
    so let's used the simplest method.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (6).svg>)

    Notes:

    Assuming Miner B is honest the Miner A needs to choose between a payoff of 4 or 0.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (7).svg>)

    Notes:

    He ofc chooses 4 as it's higher.\
    We temporarily mark it with the red circle.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (8).svg>)

    Notes:

    Same reasoning for B being dishonest and A chooses 2 over 0.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (9).svg>)

    Notes:

    Now we reverse the assumptions and assume A is honest and then B chooses between 4 and 0.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (10).svg>)

    Notes:

    Similarly as before he should choose 4 as it's higher.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (10b).svg>)

    Notes:

    And the last remaining options will result in the circled 2.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (12).svg>)

    Notes:

    Now the square with all the options circled is the Nash Equilibrium.\
    In our case it seems to be being honest.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (13).svg>)

    Notes:

    Not a big surprise, and being dishonest lands you with zero coins so it was too be expected.\
    But what if we change the assumptions a bit?

    \---v

    ### Nash Equilibrium

    \
    What does it mean exactly to be **dishonest**?\
    \
    There are some mainstream rules (the protocol) and if an individual miner breaks them it seems like an isolated\
    mistake or an attempt at cheating.\
    \


    If multiple miners break the protocol **in the same way**, it can be seen as a new protocol deviating from\
    the main one.

    Notes:

    We were assuming that miners are either honest or dishonest, but what does being DISHONEST actually mean?

    \=fragment=

    There are some mainstream rules (the protocol) and if an individual miner breaks them it seems like an isolated mistake or an attempt at cheating.\
    This is what we were analyzing before.

    \=fragment=

    But what if multiple miners break the protocol in the same way? It can be seen as a new protocol deviating from the main one.\
    And that's what we'll be looking at next.\
    The dishonest miners are cooperating.

    \---v

    ### Nash Equilibrium

    **Assumptions:**

    * Only 2 miners
    * Block reward = 2
    * Difficulty scales with number of honest miners
    * Token price scales quadratically wih the number of honest miners
    * Miners are rational actors
    * Decision between which protocol to follow

    ![Payoff Table](<img/nash.drawio (14).svg>)

    Notes:

    Assumptions are pretty much the same but this time around the dishonest miners will cooperate.\
    Effectively they will be following a different modified protocol.

    So we will no longer consider them dishonest but they simply follow a different set of rules.\
    Now miners choose to mine for the bitcoin BTC protocol or the bitcoin cash BCH protocol.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (15).svg>)

    Notes:

    Let's quickly fill up this table with the same rules as before.\
    Only this time of both miners follow BCH they ofc get the rewards in the BCH token.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (16).svg>)

    Notes:

    Just as before we take the extra step and apply the network effect.\
    If both miners secure the network price is 4 and if only 1 the price is 1.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (17).svg>)

    Notes:

    Here we have all the prices adjusted.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (18).svg>)

    Notes:

    Now let's take a look at what happens if Miner B miners BTC.\
    Miner A would prefer to also mine bitcoin.\
    So they are both mining the same thing.

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (19).svg>)

    Notes:

    On the other hand if miner B mines BCH then it seems that Miner A prefers to mine BCH...

    \---v

    ### Nash Equilibrium

    ![Payoff Table](<img/nash.drawio (20).svg>)

    Notes:

    And in fact what we have in here is two distinct Nash Equilibria!

    \---v

    ### Nash Equilibrium

    So is being honest the best strategy?

    \
    \


    Not always.\
    If the majority of people are honest then honesty pays off.\
    If the majority of people are _dishonest_ in the\
    same way then be _dishonest_ with them.

    \
    \
    In fact it was proven that in PoW following the majority is the true Nash Equilibrium no matter what\
    strategy/protocol they are using as long as it's consistent.

    Notes:

    So is being honest the best strategy?

    \=fragment=

    Not always.\
    If the majority of people are honest then honesty pays off.\
    If the majority of people are _dishonest_ in the same way then be _dishonest_ with them.

    \=fragment=

    In fact it was proven that in PoW following the majority is the true Nash Equilibrium no matter what strategy/protocol they are using as long as it's consistent.\
    So Bitcoin mining is in fact a huge coordination game and this is why honesty AKA following the BTC protocol usually pays off.

    * More complex examples will be explored later in the forks lecture on Friday
    * Paper investigating PoW Nash Equilibrium and following the majority:[https://citeseerx.ist.psu.edu/document?repid=rep1\&type=pdf\&doi=7bf78054192d98e999edcdf08971a5eed42518d2](https://citeseerx.ist.psu.edu/document?repid=rep1\&type=pdf\&doi=7bf78054192d98e999edcdf08971a5eed42518d2)

    ## Schelling Point

    Notes:

    On that topic...\
    What if we have multiple Nash Equilibria? Schelling point often comes to the rescue.

    \---v

    ### Schelling Point

    * A solution that people tend to choose (easiest to coordinate on)
    * Generally it is also a Nash Equilibrium
    * How in the world can it be useful in Blockchain?

    Notes:

    So first a Schelling point is a strategy people tend to choose.\
    It is generally a Nash Equilibrium

    \=fragment=

    But how in the world is it useful to us in Blockchain?

    \---v

    ### Schelling Point

    **Detective game**

    * Two partners in crime
    * Detective interrogates them individually

    ![Detective and 2 robbers](img/detective.drawio.png)

    Notes:

    But before we can fully answer that let's explore a different game that can show you how Schelling points work.\
    And I promise it will be applicable to Blockchain.

    So the story goes like that.\
    We have to bank robbers and a detective.\
    The detective interrogates he robbers and tries to make them confess or catch them lying.

    \---v

    ### Schelling Point

    _**Detective game**_

    ![Interrogation Game Payoff Table](img/interrogation_small.drawio.svg)

    Notes:

    If any of the robbers spill the beans and tell the truth they both loose the game and go to prison.\
    If both of them lie they get away with it.\
    Seems super simple and it should be pretty straightforward that they both simply need to lie.

    Seems like a safe strategy, right? But remember than both of them witnessed the same real events of the robbery...

    \---v

    ### Schelling Point

    _**Detective game**_

    ![Interrogation Game Large Payoff Table](img/interrogation_large.drawio.svg)

    Notes:

    But there are multiple lies they can construct.\
    If they have inconsistent stories the detective will catch them.\
    So now they need to coordinate on a specific lie and have all the details exactly the same or they are screwed.

    Contrast it with how easy it would be to just tell the truth.\
    They both witnessed the truth so talking about it in a consistent way is trivial.

    \---v

    ### Schelling Point

    _**Detective game**_

    Truthful answers are one of the easiest strategies coordinate on, so they are the Schelling Points.

    Notes:

    That's why we can say that Truthful answers are one of the easiest strategies coordinate on, so they are the Schelling Points.\
    The truth itself is a Schelling point.

    And this concept is vital to something in blockchain called...

    \---v

    ### Schelling Point

    _**Oracles**_

    Oracles are blockchain entities that provide information from the outside world to the blockchain.\
    \
    ![Oracle getting information from real world](img/oracles.drawio.svg)

    Notes:

    Oracles.\
    Firstly who in the room heard of oracles? Raise your hands.\
    Oracles are super interesting because what they are trying to achieve is to provide information from the outside world to the blockchain.\
    And that's a very very hard task.

    \---v

    ### Schelling Point

    _**Oracles**_

    Oracles are blockchain entities that provide information from the outside world to the blockchain.\
    \


    **External Information Examples:**

    * What's the temperature in Berkeley?
    * Who won the election?
    * What's the exchange rate of USD to BTC?

    Notes:

    Some examples of the information they can provide are for instance what's the current temperature in Berkeley? Who won the election? What's the exchange rate of USD to BTC? and may others.

    Let's actually see how they might work is a slightly simplified version with the temperate example.

    \---v

    ### Schelling Point

    _**Oracles**_

    \
    \
    ![Temperature Line](img/temp1.drawio.svg)

    Notes:

    So what's the temperature in Berkeley? Imagine you have a garden in Berkeley and you have on chain insurance that if the temperature is too high you get a payout.\
    So you want to know the temperature in Berkeley.

    We know the answer lies somewhere on this axis.\
    But what it is exactly?

    \---v

    ### Schelling Point

    _**Oracles**_

    \
    \
    ![Temperature Line with Some Measurements](img/temp2.drawio.svg)

    Notes:

    We can ask some users to submit what they think the temperature is.\
    Some of them will check it themselves, some will use weather apps and some will just guess.

    \---v

    ### Schelling Point

    _**Oracles**_

    ![Temperature Line with a Cluster of Measurements](img/temp3.drawio.svg)

    Notes:

    What we are hoping for is that the cluster of votes you can see here will be around the actual temperature.\
    The best approach would be to check the median.\
    And why is that?

    \---v

    ### Schelling Point

    _**Oracles**_

    * Honest participants are naturally coordinated
    * Attackers could try to coordinate and lie

    ![Temperature Line with a Cluster of Measurements](img/temp3.drawio.svg)

    Notes:

    Honest voters are naturally coordinated.\
    They will check the temperature and vote honestly all within some small margin of error.

    People that would lie to skew the results and would submit random values generally wouldn't cluster like the honest voters.\
    To make a more dangerous attack they would need to strategically coordinate on a specific value and all lie about it.\
    It's much harder to pull of than simply checking the temperature outside.

    Submitting the truth is the Schelling Point in here and it makes it easy to be honest.

    \---v

    ### Schelling Point

    _**Oracles**_

    What to do with attackers?![Temperature Line with a Cluster of Measurements](img/temp3.drawio.svg)

    Notes:

    But what if there are some attackers? What can we do about them?

    \---v

    ### Schelling Point

    _**Oracles**_

    What to do with attackers?\
    \
    If they go unpunished they can repeat the attack until successful![Temperature Line with a Cluster of Measurements](img/temp3.drawio.svg)

    Notes:

    If we never punish them they can repeat the attack until they are successful.\
    And that's not good.

    \---v

    ### Schelling Point

    _**Oracles**_

    What to do with attackers?\
    \
    If they go unpunished they can repeat the attack until successful\
    \
    Or even worse, they can make a million fake identities and spam incorrect votes![Temperature Line with a Cluster of Measurements](img/temp3.drawio.svg)

    Notes:

    Or even worse, they can make a million fake identities and spam incorrect votes.\
    So we need to punish them.

    But this is no longer a problem of a Schelling Point.\
    The Schelling point did its job already.\
    What we are talking about right now are...

    ## Incentives

    Notes:

    Incentives.\
    Incentives are the next big topic we will be exploring.\
    And they are vital to the blockchain space.

    \---v

    ### Incentives

    _"Something that encourages a person to do something."_\
    \


    In our case we want to shape incentives that motivate the users to submit honest values.

    Notes:

    Incentives are things that encourage people to do something.

    \=fragment=

    In our case we want to shape incentives that motivate the users to submit honest values.\
    We need to build out incentives in a way that shapes the expected behavior of the users to honesty.

    \---v

    ### Incentives

    _**Oracles**_

    What to do with attackers?\
    \
    If they go unpunished they can repeat the attack until successful\
    \
    Or even worse, they can make a million fake identities and spam incorrect votes![Temperature Line with a Cluster of Measurements](img/temp3.drawio.svg)

    Notes:

    So going back to our oracle problem how can we deal with attackers?

    \---v

    ### Incentives

    _**Oracles**_

    What to do with attackers?\
    \
    If they go unpunished they can repeat the attack until successful\
    \
    **Or even worse, they can make a million fake identities and spam incorrect votes**![Mask](img/mask.svg)

    Notes:

    Let's focus on the second issue of fake identities.\
    How can we prevent that?

    \---v

    ### Incentives

    _**Oracles**_

    **Sybil Attacks**\
    \
    Common problem in blockchain.\
    \
    If deploying on a chain, an easy solution is to make users lock some funds.![Mask](img/mask.svg)

    Notes:

    An attack where a single entity creates multiple fake identities is called a sybil attack and is super common in blockchain.\
    This is one of the things you always will need to ask yourself when you deploy things in blockchain.\
    Is whatever I built safe from Sybil Attacks?

    \=fragment=

    One easy ready solution that is often used is making users lock some funds.\
    Only a user with some funds locked can vote.\
    The strength of the vote is proportional to the stake so making a million accounts makes no sense.\
    This is a very simple solution but it's not always applicable.

    \---v

    ### Incentives

    _**Oracles**_

    What to do with attackers?\
    **If they go unpunished they can repeat the attack until successful**\
    \
    Or even worse, they can make a million fake identities and spam incorrect votes![Gavel Hammer](img/gavel.svg)

    Notes:

    Now let's go back to the first issue of unpunished attackers.\
    How can we deal with them so they don't continue attacking us?

    \---v

    ### Incentives

    _**Oracles**_

    **Punishments**\
    \
    We already laid out the foundation for punishments.\
    \
    Our solution for de-sybiling users makes them lock funds.\
    \
    If such a user would vote incorrectly, we can slash their funds.![Gavel Hammer](img/gavel.svg)

    Notes:

    Interestingly we already laid out the foundation for the defense.\
    Voters have some funds locked in the system so they have Skin in the game.

    \=fragment=

    If they vote incorrectly we can slash their funds.\
    This is a very common solution in blockchain.\
    Incorrect in that case would be very far from the median.

    We have designed some protective incentives and now the system seems safe.

    \---v

    ### Incentives

    _**Oracles**_

    \
    Did we forget about something?

    \
    \


    **Why would anyone participate in this system?**

    Notes:

    But did we forget about something? Anyone has any idea what it might be? What we are missing?

    \=fragment=

    Why would anyone participate in this system? Why would anyone vote? Why would anyone lock their funds and take the risk?

    \---v

    ### Incentives

    _**Oracles**_

    **Ghost Town**\
    \
    No user wants to participate\
    \
    Getting information from the real world is an effort and they voters are doing the protocol a service![Ghost](img/ghost.svg)

    Notes:

    Getting information from the real world is an effort and they voters are doing the protocol a service.\
    So we need to incentivize them to participate.\
    We need a rewards scheme or otherwise the network will be a ghost town.

    \---v

    ### Incentives

    _**Oracles**_

    **Reward Scheme**\
    \
    If users are doing the protocol a service they need to be rewarded\
    \
    One way to do it is to mint some token rewards for well-behaved voters\
    Or distribute them from a previously acquired pool of rewards![Hand receiving some money](img/rewards.svg)

    Notes:

    If users are doing the protocol a service they need to be rewarded.

    \=fragment=

    One way to do it is to mint some token rewards for well-behaved voters.

    \=fragment=

    Or distribute them from a previously acquired pool of rewards.

    But what is crucial here the protocol is safe and dependable only if there is enough voters so the incentives need to be designed in a way that encourages participation.

    More precisely, incentives need to be roughly proportional to the value an attacker could gain by compromising the system.\
    Low-stakes oracles don't need to have super aggressive incentives.

    \---v

    ### Incentives

    _**Oracles**_

    **Reward Scheme Question**\
    \
    Can we distribute fixed value rewards for correct votes?\
    Correct vote = 10$\
    \
    No.\
    We should base rewards on the size of the voter's stake.![Raised Hands](img/questions.svg)

    Notes:

    Let's do a quick question.\
    Can we distribute fixed value rewards for correct votes? As an example each Correct vote = 10$

    \=question time=

    \=fragment=

    No.\
    We should base rewards on the size of the voter's stake.\
    Otherwise the system is vulnerable to sybil attacks.\
    If you have a million fake identities you can vote a million times and get a million times the reward.\
    So the reward should be proportional to the stake.

    \---v

    ### Incentives

    **In summary:**

    * Make it easy to honest users and hard for attackers
    * Service to the protocol needs to be rewarded
    * Destructive or interfering actions need to be punished
    * De-Sybiling the users can help defend against spam

    Notes:

    Now let's summarize the main points.

    We need to make it easy for honest nodes and hard for attackers.\
    The Schelling Point as the foundational part of the design handles that for us.

    \=fragment=

    Service to the protocol needs to be rewarded.\
    We need to incentivize participation to guarantee reliable results.

    \=fragment=

    Destructive or interfering actions need to be punished.\
    We need to disincentivize bad behavior.\
    In our case we did the slashes.

    \=fragment=

    De-Sybiling the users can help defend against spam.

    We we have all of that our systems should be properly incentivized and safe...\
    and on that note what happens when the incentives are...

    ## Misaligned Incentives

    Notes:

    Misaligned.\
    When they promote some behavior that is not good for the network.

    \---v

    ### Misaligned Incentives

    _**Ethereum State Storage Issue**_

    ![Ethereum Logo](img/eth.svg)

    Notes:

    Let's take a look at Ethereum.\
    Ethereum is a blockchain that has a lot of smart contracts.\
    And smart contracts are basically programs that run on the blockchain.\
    They are stored on chain and they can be executed by anyone.\
    For them to work a bunch of code needs to be deployed on the chain.

    \---v

    ### Misaligned Incentives

    _**Ethereum State Storage Issue**_

    \
    **State Storage Replication**\
    \
    Whenever we store something on chain (like a smart contract) it needs to be at least partially replicated among the nodes.\
    \
    Multiple nodes store the same data.![Data Replication Diagram](img/replication.drawio.svg)

    Notes:

    And moreover whenever we store something on chain (like a smart contract) it needs to be at least partially replicated among the nodes.\
    Thousands of nodes store the same data which is not super efficient.

    \---v

    ### Misaligned Incentives

    _**Ethereum State Storage Issue**_

    \
    **State Storage Replication Costs**\
    \
    Ethereum deals with the burden of replication by charging more gas for submitting bulky data.\
    \
    All of that is ON TOP OF any computation gas costs.![Stacks of coins next to data blobs](img/storage_costs.drawio.svg)

    Notes:

    Ethereum attempts to deal with it by introducing scaling fees.\
    The more data you put in the state the more you need to pay.\
    And that's on top of any computation costs.

    \---v

    ### Misaligned Incentives

    _**Ethereum State Storage Issue**_

    \
    **State Storage Duration**\
    \
    This particular part of the state might be relevant for future state transitions so nodes cannot simply discard it.\
    \
    Full nodes need to keep ALL the data.![Data same over time](img/data_no_changes.drawio.svg)

    Notes:

    Note that once we put something in state it has to stay there pretty much indefinitely until we use it again.\
    Because who knows, it might be relevant to some future state transitions.\
    So nodes cannot simply discard it.

    Now let's explore an example.

    \---v

    ### Misaligned Incentives

    _**Ethereum State Storage Issue**_

    \
    **Meet Bob**\
    \
    Bob happily deploys his awesome smart contract in Ethereum.\
    He paid a hefty gas fee but so be it.\
    \
    ![Deploying a smart contract on chain](img/smart_contract.drawio.svg)

    Notes:

    So let's meet Bob.\
    Bob is a developer and he happily deploys his awesome smart contract in Ethereum.\
    He paid a hefty gas fee but so be it.\
    His code was added to the state and now many nodes hold a copy of it.

    \---v

    ### Misaligned Incentives

    _**Ethereum State Storage Issue**_

    \
    **The Problem**\
    \
    Bob decided to become a musician or just no longer likes programming.\
    \
    He doesn't care about his smart contract anymore.![Smart contract deployed on chain](img/smart_contract_deployed.drawio.svg)

    Notes:

    But imagine that one day Bob decides to become a musician or he just no longer likes programming.\
    He doesn't care about his smart contract anymore.\
    But the chain doesn't know about it.\
    His code still lives in the state and has to be continuously replicated and maintained.

    \---v

    ### Misaligned Incentives

    _**Ethereum State Storage Issue**_

    \
    **The Problem Made Worse**\
    \
    Many others like Bob follow suit.\
    \
    Some of them continue developing but, **why bother** removing old data? They already paid for it.![Many smart contracts deployed on chain](img/smart_contract_many.drawio.svg)

    Notes:

    Now imagine there are hundreds of people like Bob.\
    Some of them even continue developing but, WHY BOTHER removing old data? They already paid for it.\
    And some of them just don't care anymore.

    \---v

    ### Misaligned Incentives

    _**Ethereum State Storage Issue**_

    \
    &#xNAN;**"Why Bother?"**\
    \
    Getting data on chain is expensive, but there is no incentive to clean it up.\
    \
    This is a core misalignment of incentives that lead to Ethereum state size growing out of control.![Many smart contracts deployed on chain](img/smart_contract_many.drawio.svg)

    Notes:

    We need to focus on this "why bother" part.\
    This is a core example of a misalignment of incentives that lead to Ethereum state size growing out of control.

    Getting the data to state is indeed expensive but once we do...\
    why clean it? There is no incentive to do so.\
    So the chain was getting overwhelmed in junk.

    \---v

    ### Misaligned Incentives

    _**Ethereum State Storage Issue**_

    \
    **The Goal**\
    \
    Design new protocol rules that shape the behavior of the users in a way that they start cleaning up the state.![Cleaned smart contracts on chain](img/smart_contract_clean.drawio.svg)

    Notes:

    So what can we do about it? What's the goal? We need to design new protocol rules that shape the behavior of the users in a way that they start cleaning up the state.\
    Hopefully without any side effects.

    \---v

    ### Misaligned Incentives

    _**Ethereum State Storage Issue**_

    \
    **The Solution**\
    \
    State Storage Gas Refunds\
    \
    Pay a hefty fee when deploying data to state, but get some of it refunded when removing it.![Burning a smart contract](img/smart_contract_burn.drawio.svg)

    Notes:

    One of the proposed solutions was the introduction of a Gas Refund.\
    You pay a hefty fee when deploying data to state, but get some of it refunded when removing it.\
    So now there is an incentive to clean up the state.

    \---v

    ### Misaligned Incentives

    _**Ethereum State Storage Issue**_

    \
    \
    **behavior Before**

    ![Developer becoming a musician](img/developer_musician.drawio.svg)

    Notes:

    So what we had originally is Bob paid for his smart contract and then simply went away to play a guitar.

    \---v

    ### Misaligned Incentives

    _**Ethereum State Storage Issue**_

    \
    \
    **behavior After**

    ![Developer removing his contract and becoming a musician](img/developer_musician2.drawio.svg)

    Notes:

    Afterwards Bob deploys his contract in the same way but before running of to play a guitar he removes it from the state and gets some of the gas back.\
    He likes the extra money so he has an incentive to clean.\
    In here we're presenting the version where he recovers the full value for educational purposes but Ethereum only refunds a portion of the gas.

    But wait...\
    So what is the actual cost if he paid 10 and got 10 back? Anyone has any idea? Cost might not be obvious but it is an...

    ## Opportunity Cost

    Notes:

    Opportunity Cost.\
    It's a very important concept in economics and it's also crucial in blockchain.

    \---v

    ### Opportunity Cost

    _"The loss of other alternatives when one option is chosen."_

    ![Multiple alternatives with opportunity cost](img/opp_cost.drawio.svg)

    Notes:

    d\
    Generally opportunity cost is the loss of other alternatives when making a choice.\
    When choosing between 10 and 30$ the opportunity cost of picking 30 is 10, the other option you are forgoing.

    \---v

    ### Opportunity Cost

    _**Ethereum State Storage**_

    \
    **The Real Cost**\
    \
    Instead of having the funds locked in the storage deposit/refund scheme, Bob could have invested them somewhere else and gain some profit.\
    \
    Just locking your funds is sort of a punishment by itself.![Locking Funds vs Investing](img/opp_cost_locking.drawio.svg)

    Notes:

    Going back to the topic of Ethereum the real cost for Bob is not the 10$ he paid for storage as he regains it later.\
    The cost is in losing the opportunity of investing the money elsewhere.

    \=fragment=

    Just locking your funds is sort of a punishment by itself.\
    Even if you regain them later.\
    This is especially true in inflationary systems, and spoiler alert that most of them.

    The opportunity cost is a clever mechanism that allows us to include costs without directly charging them, and we also need to be super aware so we don't accidentally punish the users by not thinking of some external opportunity costs.

    \---v

    ### Opportunity Cost

    _**Extra Examples**_

    * Creating invalid blocks in Bitcoin never gets directly punished even if the block is rejected by the network.\
      The real cost is the opportunity cost, as the miner could have mined a valid block instead.
    * Polkadot native token DOT is inflationary (\~7.5% per year) but it can be staked to earn rewards (\~15% per year).\
      Not staking DOT has an opportunity cost which incentives staking to secure the network.

    Notes:

    There is a lot of awesome examples of opportunity costs in blockchain.\
    For instance Creating invalid blocks in Bitcoin never gets directly punished even if the block is rejected by the network.\
    The real cost is the opportunity cost, as the miner could have mined a valid block instead.

    \=fragment=

    and the Polkadot native token DOT is inflationary (\~7.5% per year) but it can be staked to earn rewards (\~15% per year).\
    Not staking DOT has an opportunity cost which incentives staking to secure the network.

    And there are also many other staking and DeFi examples out there.

    ## Externalities

    Notes:

    Now to actually appreciate what the we did in the previous section we need to talk about externalities.

    \---v

    ### Externalities

    _"A consequence of an economic activity that is experienced by unrelated third parties."_

    Notes:

    An externality is a consequence of an economic activity that is experienced by some third parties.

    As an example, think of the pollution you emit when driving a car.\
    It's a negative externality that affects all the people around you.\
    Alternatively imagine planting a tree in your garden simply because you like how it looks and gives you some shade.\
    The tree improves the quality of air in the neighborhood and that's a positive externality for the people around you.

    \---v

    ### Externalities

    _**Ethereum State Storage**_

    The clogging of the chain with useless data is a negative externality that affects all the users of the chain.

    As protocol designers we need to be aware of such externalities and we can try and limit their effects by **pricing them in**.

    Notes:

    In the Ethereum example you could argue that the network getting clogged is the externality of the single developer not cleaning after himself.\
    And it affects all the users of the chain.\
    The chain is an example of a common good.

    As protocol engineers or system designers you need to identify those externality costs and price them in.

    \---v

    ### Externalities

    _**Ethereum State Storage**_

    \
    **Negative Externality Cost**\
    \
    In the Ethereum State Storage problem we priced in the negative externality as the opportunity cost of locking your funds.![Lucking Funds vs Investing](img/opp_cost_locking.drawio.svg)

    Notes:

    That's what we did with the opportunity cost in Ethereum.\
    We made it so burdening the chain is actually expensive for the perpetrator.\
    We aligned his incentives with the incentives of the chain.

    \---v

    ### Externalities

    _**Oracles**_

    \
    **Positive Externality**\
    \
    Providing the voting services in the Oracle scheme can be seen as a positive externality for the network that can further use this extra information.\
    \
    The voters are providing a valuable service to the protocol.![Information from the external world entering Blockchain](img/oracles.drawio.svg)

    Notes:

    But not all externalities are negative.

    For example the whole oracle scheme makes it so the chain can get information from the real world.\
    This is a positive externality for the network that can further use this extra information.

    \---v

    ### Externalities

    _**Oracles**_

    The voters are providing a valuable service to the protocol.

    So if they submit the vote on chain through a transaction, should they pay any fees?

    Notes:

    The honest voters are providing a valuable service to the protocol.

    \=fragment=

    So having that mind should they pay any transaction fees when submitting votes?

    \---v

    ### Externalities

    _**Oracles**_

    \
    **Beneficial Transactions**\
    \
    Such a transaction can be totally free.\
    \
    But make sure it cannot be spammed!![Sticker with Free on it](img/free.svg)

    Notes:

    And contrary to the common belief such a transaction can be totally free.

    \=fragment=

    But make sure it cannot be spammed! And it's super important, because if it is free it can be trivial.\
    In our oracle system we can make sure there is only ONE vote per stake.\
    This way we remain safe and can make the transaction free to further incentivize participation.

    \---v

    ### Free Transactions

    \
    There are other free transactions that are not necessarily positive externalities.\
    \
    **Inherent Transactions**

    * Block rewards in BTC
    * Any logic that needs to be executed for every block (is inherent to the block)

    ![Sticker with Free on it](img/free.svg)

    Notes:

    There are other free transactions that are not necessarily positive externalities.\
    For instance in Bitcoin after mining a block you get a reward.\
    This is a free transaction that is not a positive externality.\
    It's just inherent to the block.\
    Usually any logic that needs to be executed for every block (is inherent to the block) is free.

    ## Complete vs Partial Information Games

    Notes:

    Now let's look at something totally different.\
    We will talk about a concept crucial to game theory and that is information.

    \---v

    ### Complete vs Incomplete Information Games

    _Do players know everything about the game state?_

    _Do players **NEED** to know everything about the game state?_

    Notes:

    We'll be looking at questions like do players know everything about the game state? Do they NEED to know everything about the game state? And how does it affect the game?

    \---v

    ### Complete vs Incomplete Information Games

    _**Polkadot Approval Voting (Simplified)**_

    ![Five validators and three approval checkers among them](img/Approval_checkers.drawio.svg)

    Notes:

    To investigate this topic we'll dive deeper into Polkadot and particularly the Approval Voting subsystem.\
    This is something I personally work on at Parity and you will learn a lot more about it in the later modules.

    What you need to understand now is that there are some special nodes called validators.\
    They as they name suggests validate if the new blocks in the network are valid and correct.

    \---v

    ### Complete vs Incomplete Information Games

    _**Polkadot Approval Voting (Simplified)**_

    \
    **Approval Checkers**\
    \
    In Polkadot when new blocks are validated, not everyone does the work.\
    Only some randomly chosen validators - called **Approval Checkers** - are selected to validate candidate blocks.![Five validators and three approval checkers among them](img/Approval_checkers.drawio.svg)

    Notes:

    But in Polkadot not every validator does all the work.\
    They share the work and each block is checked only by a subset of validators.\
    They are called Approval Checkers.

    \---v

    ### Complete vs Incomplete Information Games

    _**Polkadot Approval Voting (Simplified)**_

    \
    **Attackers**\
    \
    We assume that attackers can DDoS some but not ALL Validators.\
    \
    Being DDoS'ed makes them unable to vote in time.![Attackers eliminated some validators](img/validators_attack.drawio.svg)

    Notes:

    We also need to make some assumptions about the attackers willing to disrupt the network.\
    We assume that attackers can DDoS some but not ALL Validators.\
    Being DDoS'ed makes them unable to vote in time.

    \---v

    ### Complete vs Incomplete Information Games

    _**Polkadot Approval Voting**_

    **Default Scenario**

    * Randomly select 3 Approval Checkers and announce them
    * Approval Checkers publish votes if they are selected
    * If all the votes received confirm the block is fine it passes

    ![Five validators and three approval checkers among them](img/Approval_checkers.drawio.svg)

    Notes:

    A default validation scenario would go like that.\
    We randomly select 3 Approval Checkers and announce them.\
    Approval Checkers publish votes if they are selected.\
    If all the votes received confirm the block is fine it passes.

    But there is a problem with it? Does anyone know what it is?

    \---v

    ### Complete vs Incomplete Information Games

    _**Polkadot Approval Voting**_

    **Default Scenario**

    * Randomly select 3 Approval Checkers and announce them
    * Approval Checkers publish votes if they are selected
    * **Attackers use the information and DDoS the selected before they publish the vote** (except their insider)
    * If all the votes received confirm the block is fine it passes

    ![Eliminated approval checkers](img/validators_target_attack.drawio.svg)

    Notes:

    If the attackers learn who the designated approval checkers are they can focus their attack.\
    And only eliminate the relevant targets thus compromising the network.

    \---v

    ### Complete vs Incomplete Information Games

    _**Polkadot Approval Voting**_

    **What was the Problem?**

    * Attackers learned everything about the game
    * Attackers could use this information before the validators could respond

    **How do we fix it?**

    * Limit the information the attackers have access to so they cannot plan ahead

    Notes:

    So let's ask ourselves what was the problem? The attackers learned everything about the game and could use this information before the validators could respond.\
    The information is the weapon.

    \=fragment=\
    If we could somehow limit the information the game would change in our favour.\
    We need to make this a game of incomplete information, where some things are hidden.

    \---v

    ### Complete vs Incomplete Information Games

    _**Polkadot Approval Voting**_

    **Improved Scenario**

    * Each validator uses a VRF to generate a random number
    * Validators with a sufficiently small number will have the right to be Approval Checkers
    * Approval Checkers reveal themselves by showing their low numbers and publish a vote at the same time
    * If all the votes received confirm the block is fine it passes

    \


    Notes:

    * Let's imagine this new improved scenario.\
      Each validator uses a VRF to generate a random number.
    * There is some threshold and validators with a sufficiently small number will have the right to be Approval Checkers.

    \=fragment=

    * Approval Checkers reveal themselves by showing their low numbers (with a vrf proof attached) and publish a vote at the same time.\
      If all the votes received confirm the block is fine it passes.

    This method has this nice property that attackers don't learn who the approval checkers are until they reveal themselves.\
    So they cannot plan ahead.

    \---v

    ### Complete vs Incomplete Information Games

    _**Polkadot Approval Voting**_

    **What can the Attackers do?**

    * They no longer know who the Approval Checkers are so they have to guess
    * If they don't guess correctly they get heavily slashed

    ![Some validators are eliminated](img/validators_random_attack.drawio.svg)

    Notes:

    So what can the attackers do? If they can no longer target DDoS they only can attack at random.\
    This vastly reduces their chances of success and makes thm vulnerable to punishment if they fail.

    This is pretty much the method used in Polkadot and it's called a VRF based random assignment.\
    It's a game of incomplete information.

    \---v

    ### Complete vs Incomplete Information Games

    _**Extra Examples**_

    * BABE is a Polkadot mechanism for selecting new block producers (further covered in Polkadot module).\
      It also uses a similar VRF scheme to generate random assignments

    Notes:

    Some other notable examples you will learn about in later modules are connected to BABE the Polkadot mechanism for selecting new block producers.\
    It also uses a similar VRF scheme to generate random assignments.

    ## Shifting Assumptions

    Notes:

    By now you might have noticed a pattern that usually we have a list of assumptions.

    \---v

    ### Shifting Assumptions

    Every game has some assumptions that need to be made before reasoning about them.

    * Number of players
    * Available actions
    * Access to information
    * etc

    ![Board with assumptions](img/assumptions.drawio.svg)

    Notes:

    Some of the assumptions are connected to the number of players or maybe the access to information.\
    And they are usually pretty stable.

    \---v

    ### Shifting Assumptions

    If any of the assumptions change the game changes as well.\
    Old incentives that were previously sensible may now motivate a vastly different behavior.![Some of the assumptions on the board change](img/assumptions_change.drawio.svg)

    Notes:

    What happens when for some reason the assumptions evolve and change?\
    The game changes as well.\
    Old incentives that were previously sensible may now motivate a vastly different behavior.

    \---v

    ### Shifting Assumptions

    _**Restaking**_

    Restaking through EigenLayer incentives Ethereum stakers to stake the same funds for multiple apps at the same time.\
    \
    The incentive game will be vastly different and the capital will effectively be leveraged (double risk and double rewards).![EigenLayer Logo](img/eigen.drawio.png)

    Notes:

    A super good example of that is what is very recently happening in Ethereum.\
    And I mean literally this month.\
    There is a new layer 2 protocol called EigenLayer that allows stakers to stake the same funds for multiple apps at the same time.\
    This is called restaking.

    This is not something natively available in Ethereum and it wasn't taken into consideration when slashes/rewards were designed.

    \---v

    ### Shifting Assumptions

    _**Restaking**_

    **Consequences**\
    \
    Restaking consequences are still not fully understood and the research is ongoing.\
    \
    Speaker Notes ("S") for further reading.![EigenLayer Logo](img/eigen.drawio.png)

    Notes:

    The consequences of restaking are still not fully understood and the research is ongoing.\
    I encourage you to read the speaker notes for further reading.\
    The whole field of blockchain incentivization and protocol design is still developing so there are many unknowns but overall I hope all the methods shown today help you in making more informed decisions later down the line.\
    Thats it...

    * Podcast: [https://www.youtube.com/watch?v=aP9f\_1v9Ulc](https://www.youtube.com/watch?v=aP9f_1v9Ulc)
    * Whitepaper: [https://2039955362-files.gitbook.io/\~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FPy2Kmkwju3mPSo9jrKKt%2Fuploads%2F9tExk4U2OdiRKGEsUWqW%2FEigenLayer\_WhitePaper.pdf?alt=media\&token=c20ac4bd-badd-4826-9fb6-492923741c9e](https://2039955362-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2FPy2Kmkwju3mPSo9jrKKt%2Fuploads%2F9tExk4U2OdiRKGEsUWqW%2FEigenLayer_WhitePaper.pdf?alt=media\&token=c20ac4bd-badd-4826-9fb6-492923741c9e)

    ### Summary

    * Markets - Fee Markets
    * Nash Equilibrium - BTC Mining
    * Schelling Point - Oracles
    * Incentivization - Oracles
    * Opportunity cost - Ethereum State Storage Refunds
    * Externalities - Ethereum State Storage and Oracles
    * Complete vs Incomplete Information Games - Polkadot Approval Voting
    * Assumptions - Restaking

    Notes:

    So to summarize we talked about:

    ## Thanks everyone!
