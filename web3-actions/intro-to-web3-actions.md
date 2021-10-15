# Intro to Web3 Actions

**Tenderly Web3 Actions** will run your code in reaction to on-chain (and some off-chain) events on your smart contracts. 

You can use Web3 Actions to create custom scenarios in order to further deepen your debugging process, create alerting patterns that are not available out-of-the-box in the [**Alerting**](../alerts/creating-an-alert/) section, automating testing or live production execution in the [**Simulator**](../simulations-and-forks/how-to-simulate-a-transaction/) and [**Forks**](../simulations-and-forks/how-to-create-a-fork/), or anything else that comes to (your) mind.

The code Web3 Actions run is called a _**function**_. Function must be written in TypeScript (or JavaScript) and runs in Node 14 runtime. Specification of events that should result in your action running is called a _**trigger**_. There are 4 types of triggers:

* **Transaction** - run your function in reaction to transactions on any network supported by Tenderly, with statuses like _as soon as transaction is mined_ or _after 10 blocks has passed_ and filters such as _emitted events_, _invoked functions_, etc.
* **Block** - run your function in reaction to block being mined on a chosen chain.
* **Webhook** - run your function by posting a payload to an endpoint.
* **Periodic** - run your function in periodic intervals or CRON.
