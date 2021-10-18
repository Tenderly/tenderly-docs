# Intro to Web3 Actions

**Tenderly Web3 Actions** will run your code in response to on-chain (and some off-chain) events, usually on your smart contracts. 

You can use Web3 Actions to create custom scenarios in order to further deepen your debugging process, create alerting patterns that are not available out-of-the-box in the [**Alerting**](../alerts/creating-an-alert/) section, automating testing or live production execution in the [**Simulator**](../simulations-and-forks/how-to-simulate-a-transaction/) and [**Forks**](../simulations-and-forks/how-to-create-a-fork.md), or anything else that comes to (your) mind.

The code Web3 Actions run is called a _**function**_. Function must be written in TypeScript (or JavaScript) and runs in Node 14 runtime. Specification of events that your action listens to is called a _**trigger**_. There are 4 types of triggers:

* **Transaction** - runs function in response to transactions on any network supported by Tenderly, with statuses like _as soon as transaction is mined_ or _after 10 blocks has passed_ and filters such as _emitted events_, _invoked methods_, etc.
* **Block** - runs your function in response to block being mined on a chosen chain.
* **Webhook** - runs your function when request is POSTed to an endpoint.
* **Periodic** - runs your function in periodic intervals or configured CRON.

{% hint style="warning" %}
You will need [**Tenderly CLI**](https://github.com/Tenderly/tenderly-cli)** **and[**`npm`**](https://www.npmjs.com)to initialize Web3 Actions.
{% endhint %}

To get started, all you have to do is run `tenderly actions init` which will lead you through setting up a project for your Web3 Actions.

{% hint style="info" %}
You can pass `--javascript` to use JavaScript instead of TypeScript
{% endhint %}

