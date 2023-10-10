---
description: >-
  Tenderly Node is a production-ready, fast, reliable, and easy-to-scale node as
  a service solution with multi-region availability.
---

# Intro to Tenderly Node

Tenderly Node is a fast, reliable, production-ready, and easy-to-scale node solution with multi-region support. It offers your read-intensive dapps uninterrupted blockchain access with instantly synced data.&#x20;

Using Tenderly Node enables you to modify, consume, and analyze blockchain data, including historical data, essential to your research, analytics, and dapp-building process. Tenderly Node is a tightly integrated part of the Tenderly development platform, giving you the right tools for building, monitoring, and improving your dapps.

The same infrastructure powering the Tenderly development platform and handling demanding read-intensive workloads is available as a plug-and-play service. This infrastructure is powered by custom and innovative architecture: we have deconstructed the monolithic general-purpose node and created a layered Tenderly Node, providing scalability, high read throughput, and data consistency and availability by design.

The all-in-one Tenderly platform supports [engineering and UX practices](../ethereum-development-workflow.md) throughout the Ethereum dapp development process. It allows developers to accelerate smart contract development by combining debugging tools with observability and infrastructure.

## Guides and References

In the Tenderly Dashboard, go to Node. You'll see a list of supported networks, with a JSON RPC access URL for each. Use the URL to connect your dapp to a network using Tenderly Node.

{% hint style="info" %}
The RPC URL contains your private access key. You must securely manage the URL and the access key. In case of a breach, you can regenerate the access key in the Tenderly Dashboard to protect against unauthorized access.
{% endhint %}

Here are useful guides to help you get started with Tenderly Node:

* [Quickstart by querying blockchain data through Tenderly Node](quickstart-query-blockchain.md), using a visual request builder in the Tenderly Dashboard, or copying the request as runnable code.
* [Get started with using Simulation RPC](../simulations-and-forks/simulation-rpc.md) capabilities of Tenderly Node, allowing you to dry-run transactions before sending them on-chain.
* Browse the [brief reference of supported JSON RPC endpoints](references/brief-json-rpc.md), with examples and method invocation scripts.
* Browse the [detailed reference of standard JSON RPC endpoints](references/detailed-json-rpc.md) supported by Tenderly Node, drilling into the structure of request and response objects.
* Browse custom [Tenderly JSON RPC endpoints](references/simulate-json-rpc.md). The custom calls extend the standard Ethereum node functionality and are found in the `tenderly_` namespace.

## Usage quota and rate-limiting

Tenderly Node usage is rate-limited, with a monthly usage quota, expressed in **Tenderly Units (TU)**. Read, write, and calculate RPC calls have different usage footprints and, thus, contribute differently to the total usage over a time period. Find out more about [usage and rate-limiting details](pricing.md).
