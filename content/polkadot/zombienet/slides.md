---
title: Zombienet
duration: 1 hour
description: Zombienet workshop
---

# Zombienet

***

## What is Zombienet?

Zombienet is an integration testing tool that allows users to _spawn_ and _test_ ephemeral substrate based networks.

***

## Why Zombienet?

Integration tests are always complex:

\


* Setup Configuration
* Port management
* Ready state off all artifacts
* Observability
* Leaking resources

\---v

## Friction to resolve

\


* Config flexibility
* Local environment
* Maintenance
* CI friendly
* Scaling
* Test-runner

\---v

## Goals

\


**Hassle free setup**

* Toml / json
* Nice defaults
* Templating lang.

**Multiple envs**

* **Local**
* **k8s**
* **podman**

**Extensible**

* Custom assertions
* Intuitive D.S.L
* Templating lang.

***

## Phases

***

### Phases

Spawn

* Custom chain-specs
* Custom command
* Port-mapping
* Parachains registration

Test

* Custom D.S.L
* Multiple assertions
* Extensible
* Custom reporting

***

### Zombienet Options

* As binary ([releases](https://github.com/paritytech/zombienet/releases))
* As library (@zombienet)
* As container (published in docker hub)
* From source ([zombienet](https://github.com/paritytech/zombienet) repo)

Notes:

* As binary: Binaries for Linux and MacOS are available in each release in Github.
* npm packages: cli, orchestrator, utils
* image: docker.io/paritytech/zombienet\
  code is available in GitHub with the instructions on how to build and run Zombienet.\
  (https://github.com/paritytech/zombienet)

\---v

#### Download Zombienet

```sh
# macOS
curl -L https://github.com/paritytech/zombienet/releases/download/v1.3.63/zombienet-macos
-o ./zombienet

# linux
curl -L https://github.com/paritytech/zombienet/releases/download/v1.3.63/zombienet-linux
-o ./zombienet

# make executable
chmod +x zombienet
```

***

## Let’s spawn a new network!

\---v

### But first, try manually…

\


* Create chain-spec (parachain)

```sh
parachain-template-node build-spec --chain local \
--disable-default-bootnode > /tmp/para.json
```

\


* Create chain-spec (relay chain)

```sh
polkadot build-spec --chain rococo-local \
 --disable-default-bootnode > /tmp/relay.json
```

Notes:

Tutorials [https://docs.substrate.io/tutorials/build-a-parachain/](https://docs.substrate.io/tutorials/build-a-parachain/)

\---v

#### Add keys\*

\


When not using --alice or --bob, you need to provide additional `aura` and `grandpa` keys and inject them into the keystore! (**per node**)

```sh
./target/release/polkadot \
key insert --base-path /tmp/node01 \
  --chain /tmp/relay.json \
  --scheme Sr25519 \
  --suri <your-secret-seed> \
  --password-interactive \
  --key-type aura
```

\


```sh
./target/release/polkadot key insert \
  --base-path /tmp/node01 \
  --chain /tmp/relay.json \
  --scheme Ed25519 \
  --suri <your-secret-key> \
  --password-interactive \
  --key-type gran
```

Notes:

This step is optional if you use the dev accounts (e.g. alice, bob, charlie, dave, etc)

\---v

* Start relay chain nodes

```sh[1-2|4-10|12-18]
# create nodes dirs
  mkdir -p /tmp/relay/{alice,bob}

  ./target/release/polkadot \
  --alice \
  --validator \
  --base-path /tmp/relay/alice \
  --chain /tmp/relay.json \
  --port 30333 \
  --ws-port 9944

  ./target/release/polkadot \
  --bob \
  --validator \
  --base-path /tmp/relay/bob \
  --chain /tmp/relay.json \
  --port 30334 \
  --ws-port 9945
```

Notes:

Why do we need to use different ports for Alice and Bob?

\---v

* Start collator

```sh
# create nodes dirs
mkdir -p /tmp/para/alice

parachain-template-node \
--alice \
--collator \
--force-authoring \
--chain /tmp/para.json \
--base-path /tmp/para/alice \
--port 40333 \
--ws-port 8844 \
-- \
--execution wasm \
--chain /tmp/relay.json \
--port 30343 \
--ws-port 9977
```

\---v

* Register ParaId on relay chain

1. Modify parachain chain-spec and create raw format
2. Generate genesis wasm and state
3. Register parachain using sudo call

\


```sh[1,2|4,5|7,8]
parachain-template-node build-spec --chain /tmp/para-raw.json \
--disable-default-bootnode --raw > /tmp/para-raw.json

parachain-template-node export-genesis-wasm --chain /tmp/para-raw.json \
para-2000-wasm

parachain-template-node export-genesis-state --chain /tmp/para-raw.json \
para-2000-genesis-state
```

***

## Activity

Follow the [connect a local parachain](https://docs.substrate.io/tutorials/build-a-parachain/connect-a-local-parachain/) to launch your own network.

***

### Non-trivial chore

* Error prone.
* Multiple commands.
* Port management.
* Multiple process.

Zombienet allow you to set everything in just 1 file.

\---v

### Zombienet network definition

Zombienet allow to [define your network](https://paritytech.github.io/zombienet/network-definition-spec.html) with a simple configuration file.

Notes:

[https://paritytech.github.io/zombienet/network-definition-spec.html](https://paritytech.github.io/zombienet/network-definition-spec.html)

\---v

```toml[1|3-12|14-21]
# examples/0001-small-network.toml

[relaychain]
default_image = "docker.io/parity/polkadot:latest"
default_command = "polkadot"
chain = "rococo-local"

  [[relaychain.nodes]]
  name = "sub"

  [[relaychain.nodes]]
  name = "zero"

[[parachains]]
id = 1001
cumulus_based = true

  [parachains.collator]
  name = "collator01"
  image = "docker.io/parity/polkadot-parachain:latest"
  command = "polkadot-parachain"
```

Notes:

[https://github.com/pepoviola/zombienet-presentation-examples/blob/main/examples/0001-small-network.toml](https://github.com/pepoviola/zombienet-presentation-examples/blob/main/examples/0001-small-network.toml)

\---v

#### Spawn the network

```sh
./zombienet spawn examples/0001-small-network.toml
```

***

## Activity

Try to launch a network with `2` parachains.

\


[https://paritytech.github.io/zombienet/](https://paritytech.github.io/zombienet/)

***

### Make the network config dynamic

The network definition supports using [nunjucks](https://mozilla.github.io/nunjucks/) templating language (similar to [tera](https://github.com/Keats/tera)).\
Where \{{variables\}} are replaced with env vars and you can use all the built-in features.

\


```toml[2]
[relaychain]
default_image = "{{ZOMBIENET_INTEGRATION_IMG}}"
default_command = "polkadot"
```

\---v

### Make the network config dynamic

![](img/zombienet-env-vars.png)

***

### Providers

Zombienet providers allow to spawn and test networks with in different environments.

\---v

Kubernetes\


* Used internally, integrated with the [Grafana](https://grafana.com/oss/grafana/) stack.
* You need to provide your infra stack.

Podman\


* Automatically spawn and wire an instance of [Grafana](https://grafana.com/oss/grafana/) stack.
* Attach a jaeger instance if enabled in the network definition.

Native\


* Allow to attach to a running [Grafana](https://grafana.com/oss/grafana/) stack.**(wip)**

***

## Questions

***

### Meet the Test-runner

Zombienet’s built-in test-runner allows users to use a simple D.S.L. to easily and intuitively write tests with a set of natural language expressions to make assertions.

\---v

#### Built-in assertions

\


* Prometheus: Query the exposed metrics/histograms and assert on their values.
* Chain: Query/subscribe chain's storage/events.
* Custom scripts: Run custom js scripts or bash scripts (inside the pod).
* Node's logs: Match regex/glob patterns in the node's logs.
* Integrations: Zombienet supports multiple integrations, like jaeger spans, polkadot introspector and the backchannel.

\---v

```[1-3|6|7|14-16|18-20|22-24|26-28]
Description: Small Network Paras
Network: ./0002-small-network-paras.toml
Creds: config # Only used with k8s

# well known functions
validator: is up # check all the validators in the group
validator-0: parachain 1000 is registered within 225 seconds
validator-0: parachain 1001 is registered within 225 seconds

# ensure parachains are producing blocks
validator-0: parachain 1000 block height is at least 5 within 300 seconds
validator-0: parachain 1001 block height is at least 5 within 300 seconds

# metrics
validator-0: reports node_roles is 4
validator-0: reports block height is at least 2 within 15 seconds

# logs (patterns are transformed to regex)
validator-1: log line matches glob "*rted #1*" within 10 seconds
validator-1: log line matches "Imported #[0-9]+" within 10 seconds

# system events (patterns are transformed to regex)
validator-2: system event contains "A candidate was included" within 10 seconds
validator-2: system event matches glob "*was backed*" within 10 seconds

# custom scripts
validator-0: js-script ./custom.js with "alice" within 200 seconds
validator-0: run ./custom.sh within 200 seconds
```

Notes:

First three lines are the header

Each line represents an assertion

Each assertion is executed sequentially

Assertions on a group check each node

within keyword allows to keep-trying until time expires

***

### DSL extension

Learning a new DSL can be tedious, but if you are using vscode we develop an [extension](https://github.com/paritytech/zombienet-vscode-extension) that can help you to write test easily.

Notes:

Show the extension link[https://github.com/paritytech/zombienet-vscode-extension](https://github.com/paritytech/zombienet-vscode-extension)

***

## Demo time

```sh
./zombienet -p native test examples/0002-small-network-paras.zndsl
```

***

## Extensibility

Zombienet allow users to use the custom-js assertion to extend and run custom tests.

\---v

### Custom-js

```sh
# custom scripts
validator-0: js-script ./custom.js with "alice" within 200 seconds
```

```js
async function run(nodeName, networkInfo, args) {
  const { wsUri, userDefinedTypes } = networkInfo.nodesByName[nodeName];
  const api = await zombie.connect(wsUri, userDefinedTypes);
  const validator = await api.query.session.validators();
  return validator.length;
}

module.exports = { run };
```

Notes:

Zombienet will load your script and call the run function.

Passing the node name, network info and an array of arguments from the assertion

Your function have access to the zombie object exposing utilities like connect, ApiPromise, Keyring, etc \*

The assertions can validate the return value or the completions of your script.

\*similar to the way that scripts are written in PolkadotJS apps - developer page (https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Frpc.polkadot.io#/js)

***

### More extensibility

Zombienet also allow users to use as a library to create their own interactions with the running network.

\---v

#### As a Library

* @zombienet/orchestrator module expose the start function as entrypoint.
* Returning a [network](https://github.com/paritytech/zombienet/blob/main/javascript/packages/orchestrator/src/network.ts#L77) instance, with all the information about the running topology.
* You can also use the [test](https://github.com/paritytech/zombienet/blob/main/javascript/packages/orchestrator/src/orchestrator.ts#L853) function passing a callback to run your test.
* @zombienet/utils module expose misc utils functions like _readNetworkConfig_.

\---v

```js[1|2|6-7|10-12|14|]
import {start} from "@zombienet/orchestrator";
import { readNetworkConfig } from "@zombienet/utils";

const ZOMBIENET_CREDENTIALS = "";

// can be toml or json
const launchConfig = readNetworkConfig("../examples/0001-small-network.toml");

( async () => {
    const network = await start(ZOMBIENET_CREDENTIALS, launchConfig, {
        spawnConcurrency: 5,
    });

    // write your own test, `network` will have all the network info
})();
```

***

### The road ahead...

🚧 🚧 Zombienet v2 (a.k.a [SDK](https://github.com/paritytech/zombienet-sdk)) is currently under construction 🚧 🚧

The [SDK](https://github.com/paritytech/zombienet-sdk) will provide a set of building blocks that users can combine to spawn and interact with the network and also a fluent API for crafting different topologies and assertions for the running network.

Notes:

SDK repo: https://github.com/paritytech/zombienet-sdk

***

### Acknowledgement & Contributions

Zombienet take inspiration and some patterns from polkadot-launch and SimNet.

We encourage everyone to test it, provide feedback, ask question and contribute.

***

## Questions

***

### Activity

* Launch a network with two validators and one parachain.
* Add a test to ensure:
  * block producing
  * peers number
  * node's role

***

### Additional Resources!

> Check speaker notes (click "s" 😉)

Notes:

Zombienet:

* [repo](https://github.com/paritytech/zombienet/)
* [docs](https://paritytech.github.io/zombienet/)
* [v2 Roadmap](https://github.com/orgs/paritytech/projects/55/)
* [sub0 slides](https://docs.google.com/presentation/d/1wPjbrqLg9MCfygvBYV5gDra39cSr5TXg/edit)
* [sub0 presentation](https://www.youtube.com/watch?v=QKTZZCpdGH4)
* [Presentation examples](https://github.com/pepoviola/zombienet-presentation-examples)
* [Setting up a local testnet](https://hackmd.io/kSFS2ButRESeJ7hu_iKKoA)
