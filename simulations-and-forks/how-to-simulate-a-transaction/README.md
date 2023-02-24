---
description: >-
  Learn more about using the Tenderly Simulation UI and how to build a simple
  transaction simulation.
---

# Simulation UI

The Simulation UI gives you an IDE-like experience when simulating transactions. You can either build a transaction from scratch or load an existing transaction into Transaction Simulator, tweak the inputs, and override state variables or the smart contract code.

Replaying an existing transaction using a simulation allows you to:

* Validate bugfixes by running simulations on modified smart contract source code.
* Validate adjustments to transaction parameters to find optimal inputs.
* Troubleshoot an existing transaction, either a reverted one or a successful transaction with undesired effects.&#x20;

### Using the Simulation UI

You can use the Simulation UI to:&#x20;

* [Simulate a simple transaction](using-simulation-ui.md)
* [Set custom overrides of smart contract variables](simulation-ui-with-state-overrides.md) to impose custom conditions on the simulation.
* Progress to [using Simulation API](../simulation-api/) to do simulations programmatically.
* Explore [using Forks to simulate several transactions](../forks/).

### Building a simulation

When building a transaction simulation, you can:

* Run a simulation off of an existing transaction or build one from scratch.
* Run a simulation on changed smart contract source code.
* Specify the standard transaction fields: sender, value, as well as the smart contract function you're calling and its arguments.
* Override smart contract state variables.
* Override a block header by specifying custom **blockNumber** and **timestamp** values that the smart contract code receives.
* Specify an arbitrary sender (**from**).
* Specify an arbitrary **gas** and **gasPrice** for this particular simulation.
* Use either the latest block number or specify a historical block number.
