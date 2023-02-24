---
description: >-
  Get started with Tenderly Simulation API to integrate Transaction Simulator
  into your project.
---

# Simulation API

Simulation API allows you to understand a transaction's execution against any point in a network's history, including the latest block, without sending it to the blockchain. The API gives you access to a lightweight blockchain execution environment that delivers and persists detailed information about state changes, emitted events (logs), gas usage, and all calls that the transaction made.&#x20;

You can then use Simulation API to introduce this information to your development, enrich your dapp decision-making process, or expose it to your dapp users. Since simulations don't run on an actual network, they're also a gas-free way to test "what-if" scenarios.

### Simulation API use cases

By integrating with Simulation API, you can:&#x20;

* [Dry-run user transactions in dapps](../integration-guides/using-simulation-rpc-in-dapp-ui.md) to save money on failed transactions and improve your dapp UX by increasing visibility into transaction execution.
* [Run your dapp in playground mode](../integration-guides/dapp-playground-mode.md) to let users try out your dapp with all production data readily available and without spending any gas.&#x20;
* [Stage QA environments for a blockchain project](../integration-guides/instant-staging-qa-environment-for-dapps.md).
* [Set up CI/CD for your blockchain project](../integration-guides/ci-cd-pipeline-for-smart-contracts.md).
* Validate complex DAO governance proposals.

### Getting started with Simulation API

Simulation API enables you to simulate transactions using a single REST endpoint. It supports two modes:

* **Full simulation mode:** This mode **** gives you decoded simulation results, matched to smart contracts' code, for easier client-side interpretation. The decoded form contains information such as logs (emitted events), state changes, and function calls along the call trace.
* **Quick simulation mode:** This mode gives you raw transaction results, with a faster response.

{% content-ref url="simulation-api-quick-and-full-mode.md" %}
[simulation-api-quick-and-full-mode.md](simulation-api-quick-and-full-mode.md)
{% endcontent-ref %}

When using the **full** mode, you can easily get high details of simulation info and use it in your dapp. See the following example:

{% content-ref url="advanced-simulation-api-usage.md" %}
[advanced-simulation-api-usage.md](advanced-simulation-api-usage.md)
{% endcontent-ref %}

### Simulation bundles

Aside from using Simulation RPC and Simulation API to simulate single transactions, you can use them to **simulate a sequence of interdependent transactions**. You can achieve this using **Simulation Bundle API**:

{% content-ref url="bundled-simulations.md" %}
[bundled-simulations.md](bundled-simulations.md)
{% endcontent-ref %}

### Simulation state overrides

Use state overrides with Simulation API to set custom states for the contracts involved in a transaction before running a transaction simulation.

{% content-ref url="simulation-api-with-state-overrides.md" %}
[simulation-api-with-state-overrides.md](simulation-api-with-state-overrides.md)
{% endcontent-ref %}

