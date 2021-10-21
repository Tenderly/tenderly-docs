# Intro to Web3 Actions

**Tenderly Web3 Actions** will run your code in response to on-chain (or even off-chain) events, usually on your smart contracts.&#x20;

You can use Web3 Actions to create custom scenarios in order to further deepen your debugging process, create alerting patterns that are not available out-of-the-box in the [**Alerting**](../alerts/creating-an-alert/) section, automating testing or live production execution in the [**Simulator**](../simulations-and-forks/how-to-simulate-a-transaction/) and [**Forks**](../simulations-and-forks/how-to-create-a-fork.md), or anything else that comes to (your) mind.

The code Web3 Actions run is called a _**function**_. Function must be written in TypeScript (or JavaScript) and runs in Node 14 runtime. Specification of events that your action listens to is called a _**trigger**_. There are 4 types of triggers:

* **Transaction** - runs function in response to transactions, with statuses like _as soon as transaction is mined_ or _after 10 blocks has passed_ and filters such as _emitted events_, _invoked methods_, etc.
* **Block** - runs your function when block is mined on a chosen chain(s).
* **Webhook** - runs your function when request is POSTed to an endpoint.
* **Periodic** - runs your function in periodic intervals or configured CRON.

### Getting Started

To get started,  run `tenderly actions init` which will lead you through setting up a project for your Web3 Actions.

{% hint style="warning" %}
You will need [**Tenderly CLI**](https://github.com/Tenderly/tenderly-cli)** **initialize Web3 Actions. You will need [**npm**](https://www.npmjs.com) if you are using TypeScript actions or you can pass `--javascript.`
{% endhint %}

After initialization, project contains:

* `tenderly.yaml` with specification of all actions (e.g. name, description, etc.) and their triggers. For more details, see [configuration](https://app.gitbook.com/o/-LeLQOwIQG3HndcULLU2/s/-LeLQaB11\_TIOtLg8tIW/c/CdQUNwVtK1HwdPK4UIfp/web3-actions/configuration) page.
* `actions` directory (or whatever is chosen during setup) where functions implementation should go including files `package.json` or `tsconfig.json` in case of TypeScript.

{% hint style="warning" %}
All `tenderly actions` commands must be run from directory that contains `tenderly.yaml.`
{% endhint %}

### Deploying Actions

To view your actions in dashboard, you must deploy them first. Run `tenderly actions deploy` in initialized project to deploy generated example and go to provided link to view action in dashboard. If you just want to validate configuration or build implementation without deploying it, run `tenderly actions build`.

### Manual Trigger

While action must specify trigger type, it doesn't have to configure trigger. Without configured trigger, action will never run automatically. But you can still run your action manually! This can be useful for testing. Navigate to the specific action and click the **Manual Trigger** button. You can provide any payload you want, as long as it matches the required schema.



Next, we are going to describe how to write a function and what runtime features are available.
