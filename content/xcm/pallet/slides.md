---
title: XCM Pallet
duration: 1 hour
description: Introduction to `pallet-xcm`, its interface and features implemented here.
---

# XCM Pallet

***

#### Lesson goals:

* Understand what the interface of the pallet is and its implementation.
* How versioning discovery works.
* How receiving responses work.
* Understand how to craft XCM in FRAME pallets.

***

## The XCM pallet

We have now learnt about the XCVM and FRAME.

The XCM pallet is the bridge between the XCVM subsystem and the FRAME subsystem.

**It also allows us to send/execute XCM and interact with the XCM executor**.

***

## How XCM is expected to be used

XCM is not intended to be written by end-users.

Instead, _developers_ write XCVM programs, and package them up into FRAME extrinsics.

Notes:

How do wallets wallet providers use XCM ?

We will see examples of XCM being built in the runtime when exploring `teleport_assets` and `reserve_transfer_assets` extrinsics.

***

### Key roles of `pallet-xcm`

1. Allows to interact with the `xcm-executor` by executing xcm messages.\
   These can be filtered through the `XcmExecuteFilter`.
2. Allows sending arbitrary messages to other chains for certain origins.\
   The origins that are allowed to send message can be filtered through `SendXcmOrigin`.
3. Provides an easier interface to do reserve based transfers and teleports.\
   The origins capable of doing these actions can be filtered by `XcmTeleportFilter` and `XcmReserveTransferFilter`.
4. Handles XCM version negotiation duties.
5. Handles asset-trap/claim duties.
6. And other state based requirements of the XCVM.

Notes:

* Even when the XCM pallet allows any FRAME origin to send XCMs, it distinguishes root calls vs any other origin calls.\
  In the case of the latter, it appends the `DescendOrigin` instruction to make sure non-root origins cannot act on behalf of the parachain.

***

## The XCM Pallet

`pallet-xcm` provides default implementations for many traits required by `XcmConfig`.

`pallet-xcm` also provides an interface containing 10 different extrinsics, which can be split into three categories:

* Primitive functions to locally `execute` or `send` an XCM.
* High-level functions for asset transfers between systems, e.g. teleportation and reserve asset transfers.
* Extrinsics aimed exclusively at version negotiation.

***

## `pallet-xcm` Primitive extrinsics

*   `execute`

    Direct access to the XCM executor.\
    Executed on behalf of FRAME's signed origin.

flowchart TD\
subgraph paraA\[Parachain A              .]\
executor --"success?"--> palletxcm\
palletxcm("pallet-xcm") --"execute"--> executor("xcm-executor")\
end\
execute("execute(xcm)") --> palletxcm

Notes:

It checks the origin to ensure that the configured `SendXcmOrigin` filter is not blocking the execution.\
It executes the message **locally** and returns the outcome as an event.

\---v

## `pallet-xcm` Primitive extrinsics

* `send`

Sends a message to the provided destination.

flowchart LR\
subgraph paraA\[Parachain A]\
palletxcma("pallet-xcm") --"deliver"--> routera("xcm-router")\
routera --> mqueuea("message queue")\
end\
subgraph paraB\[Parachain B]\
mqueueb("message queue") --> executorb("xcm-executor")\
end\
send("send(xcm)") --> palletxcma\
mqueuea --> mqueueb

Notes:

This extrinsic is a function to send a message to a destination.\
It checks the origin, the destination and the message.\
Then it lets the `XcmRouter` handle the forwarding of the message.

***

## `pallet-xcm` Asset Transfer extrinsics

![](../intro/img/teleport.png)![](../intro/img/reserve-tx.png)

Notes:

We have already seen what teleports and reserve transfers mean in lesson 7.1; A quick reminder.

\---v

## `pallet-xcm` Asset Transfer extrinsics

`limited_teleport_assets`

This extrinsic allows the user to perform an asset teleport.

flowchart LR\
subgraph paraA\[Parachain A]\
palletxcma("pallet-xcm") --"1. execute"--> executora("xcm-executor")\
executora --"send"--> sendera("xcm-sender")\
end\
subgraph tdestination\[Trusted Destination]\
end\
lteleport("limited\_teleport\_assets(\n  dest,\n  beneficiary,\n  assets,\n  fee\_asset\_item,\n  weight\_limit\n)"):::left --> palletxcma\
sendera --"2."--> tdestination\
classDef left text-align:left

\---v

### `limited_teleport_assets`

1. `pallet-xcm` composes the following XCM and passes it to `xcm‑executor`
2. ```rust
   Xcm(vec![
     WithdrawAsset(assets),
     SetFeesMode {jit_withdraw: true},
     InitiateTeleport {assets: Wild(AllCounted(max_assets)), dest, xcm},
   ])
   ```
3. Parachain A then sends the following message to the trusted destination
4. ```rust
   Xcm(vec![
     ReceiveTeleportedAsset(assets),
     ClearOrigin,
     BuyExecution { fees, weight_limit },
     DepositAsset { assets: Wild(AllCounted(max_assets)), beneficiary },
   ])
   ```

\---v

## `pallet-xcm` Asset Transfer extrinsics

`limited_reserve_transfer_assets`

Allow the user to perform a reserve-backed transfer from the reserve chain to the destination.

flowchart LR\
subgraph reserve\[Reserve Chain]\
palletxcma("pallet-xcm") --"1. execute"--> executora("xcm-executor")\
executora --"send"--> sendera("xcm-sender")\
end\
subgraph destination\[Destination]\
end\
lteleport("limited\_reserve\_transfer\_assets(\n  dest,\n  beneficiary,\n  assets,\n  fee\_asset\_item,\n  weight\_limit\n)"):::left --> palletxcma\
sendera --"2."--> destination\
classDef left text-align:left

\---v

### `limited_reserve_transfer_assets`

1. `pallet-xcm` composes the following XCM and passes it to `xcm‑executor`
2. ```rust
   Xcm(vec![
     SetFeesMode { jit_withdraw: true },
     TransferReserveAsset { assets, dest, xcm },
   ])
   ```
3. Reserve Chain then sends the following mesasge to the destination
4. ```rust
   Xcm(vec![
     ReserveAssetDeposited(assets),
     ClearOrigin,
     BuyExecution { fees, weight_limit },
     DepositAsset { assets: Wild(AllCounted(max_assets)), beneficiary },
   ])
   ```

***

## 🗣️ version negotiation with `pallet-xcm`

XCM is a **versioned message format**.

One version may contain more or different instructions than another, so for parties to communicate via XCM, it is important to know which version the other party is using.

The version subscription mechanism allows parties to subscribe to version updates from others.

```rust
pub enum VersionedXcm {
  V2(v2::Xcm),
  V3(v3::Xcm),
}
```

Notes:

* V0 and V1 were removed with the addition of XCM v3.

\---v

### 🗣️ version negotiation with `pallet-xcm`

But chains need to be aware of the version supported by each other.`SubscribeVersion` and `QueryResponse` play a key role here:

```rust
enum Instruction {
  // --snip--
  SubscribeVersion {
        query_id: QueryId,
        max_response_weight: u64,
  },
  QueryResponse {
        query_id: QueryId,
        response: Response,
        max_weight: u64,
  },
  // --snip--
}
```

Notes:

* `query_id` would be identical in the `SubscribeVersion` and `QueryResponse` instructions.
* Likewise, `max_response_weight` should also match `max_weight` in the response

\---v

### 🗣️ version negotiation with `pallet-xcm`

* `ResponseHandler`: The component in charge of handling response messages from other chains.
* `SubscriptionService`: The component in charge of handling version subscription notifications to other chains

```rust
impl Config for XcmConfig {
 // --snip--
 type ResponseHandler = PalletXcm;
 type SubscriptionService = PalletXcm;
}
```

Notes:

* `PalletXcm` keeps track of the versions of each chain when it receives a response.
* It also keeps track of which chains it needs to notify whenever we change our version

***

### Subscription Service

Any system can be notified of when another system changes its latest supported XCM version.\
This is done via the `SubscribeVersion` and `UnsubscribeVersion` instructions.

The `SubscriptionService` type defines what action to take when processing a `SubscribeVersion` instruction.

Notes:

`pallet-xcm` provides a default implementation of this trait.\
When receiving a `SubscribeVersion`, the chain sends back an XCM with the `QueryResponse` instruction containing its current version.

***

### Version Negotiation

The subscription service leverages any kind of exchange of XCMs between two systems to begin the process of version negotiation.

Each time a system needs to send a message to a destination with an unknown supported XCM version, its location will be stored in the `VersionDiscoveryQueue`.\
This queue will then be checked in the next block and `SubscribeVersion` instructions will be sent out to those locations present in the queue.

Notes:

SubscribeVersion - instructs the local system to notify the sender whenever the former has its XCM version upgraded or downgraded.\
UnsubscribeVersion - if the sender was previously subscribed to XCM version change notifications for the local system, then this instruction tells the local system to stop notifying the sender on version changes.

\---v

### 🗣️ XCM Version Negotiation

XCM version negotiation:

1. Chain A sends `SubscribeVersion` to chain B.
2. Chain B responds `QueryResponse` to chain A with the same query\_id and max\_weight params, and puts the XCM version in the response
3. Chain A stores chain B's supported version on storage.
4. The same procedure happens from chain B to chain A.
5. Communication is established using the highest mutually supported version.

\---v

### 🗣️ XCM Version Negotiation

In the following scenario Chain A is using XCM v2

flowchart BT\
subgraph registryA\[Chain A's Registry]\
chainB("Chain B \n\n v2")\
chainC("Chain C \n\n v3")\
chainD("Chain D \n\n v1")\
chainE("Chain E \n\n v3")\
endflowchart LR\
chainARequest("Chain A") --"Chain E ? \n\n v2"--> chainERequest("Chain E")

***

### Response Handler

Version negotiation is just one example among many kinds of queries one chain can make to another.\
Regardless of which kind of query was made, the response usually takes the form of a `QueryResponse` instruction.

\---v

### Response Handler

We have talked about XCM being asymmetric, so why are there responses ?

\---v

### Information Reporting

Every instruction used for information reporting contains `QueryResponseInfo`.

```rust
pub struct QueryResponseInfo {
    pub destination: MultiLocation,
    pub query_id: QueryId,
    pub max_weight: Weight,
}
```

Notes:

All Information Reporting instructions contain a `QueryResponseInfo` struct, which contains information about the intended destination of the response, the ID of the query, and the maximum weight that the dispatchable call function can use.\
The dispatchable call function is an optional operation that XCM author can specify, and is executed upon receiving the response, effectively acting as a lifecycle hook on response.

\---v

### Information retrieval

```rust
enum Instruction {
    // --snip--
    QueryResponse {
        query_id: QueryId,
        response: Response,
        max_weight: Weight,
        querier: Option<MultiLocation>,
    },
    // --snip--
}
```

Notes:

The above instruction is the one used for offering some requested information that the local system is expecting.`querier` parameter should be checked to ensure that the system that requested the information matches with what is expected.

***

### Asset Trap/Claims with `pallet-xcm`

What happens when there are still funds in the holding register after the execution of every instruction is done?

Any situation in which the holding register contains assets after the execution of the XCM message would lead to asset trapping.

These traps need to be **stored** to allow for future claiming of these trapped assets, FRAME provide us with means for this.

Notes:

* This is handled in the `post_execute` function of the xcm-executor.

\---v

### Asset Trap/Claims with `pallet-xcm`

* **`pallet-xcm` asset trapper**: Trapped assets are stored in the `AssetTraps` storage item and indexed by origin and assets
* **`pallet-xcm` asset claimer**: `pallet-xcm` also allows for claiming trapped assets, providing that:
  * the origin claiming the assets is identical to the one that trapped them.
  * the `Asset` being claimed is identical to the one that was trapped

Notes:

* Each map element on `AssetTraps` holds a counter of how many times such origin has trapped such `Asset`.
* Every time such `Asset` gets reclaimed, the counter decrements by one.

***

### Extrinsic breakdown

Let's jump into the code and have a look at `limited_teleport_assets` extrinsic.

[source 🔍](https://github.com/paritytech/polkadot-sdk/blob/342d720/polkadot/xcm/pallet-xcm/src/lib.rs#L1099)

***

### Summary

In this lecture, we learnt:

* What the XCM pallet is and what it's used for.
* How XCM is intended to be used, both by wallet and runtime developers.
* The useful extrinsics in the XCM pallet.
* How XCM versioning works.
* How the XCM pallet is used to receive responses.
* How assets might be trapped and how to use the XCM pallet to claim them.
