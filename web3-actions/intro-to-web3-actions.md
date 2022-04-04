# Intro to Web3 Actions

**Tenderly Web3 Actions** will run your code in response to on-chain (or even off-chain) events, usually on your smart contracts.&#x20;

You can use Web3 Actions to create custom scenarios in order to further deepen your debugging process, create alerting patterns that are not available out-of-the-box in the [**Alerting**](../alerts/creating-an-alert/) section, automating testing or live production execution in the [**Simulator**](../simulations-and-forks/how-to-simulate-a-transaction/) and [**Forks**](../simulations-and-forks/how-to-create-a-fork/), or anything else that comes to (your) mind.

The code Web3 Actions run is called a _**function**_. The function must be written in TypeScript (or JavaScript) and run in Node 14 runtime. Specification of events that your action listens to is called a _**trigger**_. There are 5 types of triggers:

* **Transaction** - runs a function in response to transactions, with statuses like _as soon as the transaction is mined_ or _after 10 blocks have passed_ and filters such as _emitted events,_ _invoked methods_, etc.
* **Block** - runs your function when the block is mined on a chosen chain(s).
* **Webhook** - runs your function when a request is POSTed to an endpoint.
* **Periodic** - runs your function in periodic intervals or configured CRON.
* **Alert** - use your action as the destination channel for an alert (trigger your action when your defined alert is triggered).

### Getting Started (CLI)

To get started,  run `tenderly actions init` in a directory where you want to initialize actions project, which will lead you through setting up a project for your Web3 Actions.

{% hint style="warning" %}
You will need [**Tenderly CLI**](https://github.com/Tenderly/tenderly-cli) **** to initialize Web3 Actions. You will need [**npm**](https://www.npmjs.com) if you are using TypeScript actions or use `tenderly actions init --language javascript.`
{% endhint %}

After initialization, the project contains:

* `tenderly.yaml` with the specification of all actions (e.g. name, description, etc.) and their triggers. For more details, see the [**configuration**](configuration.md) page.
* `actions` directory (or whatever is chosen during setup) where functions implementation should go including files `package.json` or `tsconfig.json` in the case of TypeScript.

{% hint style="warning" %}
All `tenderly actions` commands must be run from a directory that contains `tenderly.yaml.`
{% endhint %}

When you initialize actions project, you must select a Tenderly project which will be used for deploying your actions. You can deploy actions from multiple locations to the same Tenderly project. You can also initialize actions multiple times in the same directory and select a different Tenderly project for each initialization.&#x20;

{% hint style="info" %}
If your actions are very different or have different dependencies, it is recommended to separate them. You can still use the same Tenderly project to deploy them.
{% endhint %}

If your actions have dependencies, `node_modules` directory located in the same directory with your actions source files will be packaged and deployed with your actions. `npm install` must be run from a directory where actions sources are. Note that this might be a different directory than one where you run `tenderly actions` commands.&#x20;

{% hint style="warning" %}
Zipped dependencies must not exceed 45MB. Reach out to us if your requirements exceed this limit.
{% endhint %}

### Step-by-Step Guide

If you want to create your first Web3 Action and go through a step-by-step guide, we prepared for you an onboarding flow in the UI. When you go to Actions Page, you will see an onboarding flow that will help you to get started with Web3 Actions.

**Quick Guide** provides a quick overview of the steps you need to reproduce in order to deploy your first Web3 Action.

![Quick Guide](<../.gitbook/assets/Screenshot 2021-11-25 at 17.02.59.png>)

**Step-by-Step Guide** provides an in-depth explanation for each step you need to reproduce in order to deploy your first Web3 Action.

{% hint style="warning" %}
You need to import an example contract into your project in order to start the tutorial and create your Web3 Action example.\
\
If you are not using the tutorial, you don't have to do this in order to use Web3 Actions.
{% endhint %}

![Step-by-Step Guide](<../.gitbook/assets/Screenshot 2021-11-25 at 17.09.58.png>)

![Create a Function Step](<../.gitbook/assets/Screenshot 2021-11-25 at 17.08.56.png>)

![Use Secrets Step](<../.gitbook/assets/Screenshot 2021-11-25 at 17.11.27.png>)

![Configure a Trigger Step](<../.gitbook/assets/Screenshot 2021-11-25 at 17.11.31.png>)

![Deploy Action Step](<../.gitbook/assets/Screenshot 2021-11-25 at 17.11.35.png>)

### Deploying Actions

To view your actions in the dashboard, you must deploy them first. Run `tenderly actions deploy` in an initialized project to deploy generated example and go to provided link to view the action in the dashboard. If you initialized actions for multiple projects in the same directory, you will be asked to select a project which you want to deploy. All actions for a single project are deployed together.

{% hint style="info" %}
Deployed action can be stopped through the dashboard. Action will stay deployed, but it won't run automatically.
{% endhint %}

If you just want to validate configuration or build implementation without deploying it, run `tenderly actions build`.

### Create and Edit Action from the UI

If you prefer a more visual experience while setting up your actions, we created a Web3 Action UI Builder. Go to the **Actions** tab in the sidebar and click on **Add Action** button in the upper right corner.

![Web3 Actions Welcome Screen](<../.gitbook/assets/image (90).png>)

You will enter to **Web3 Action Cration** page where you can configure action type, set up code and trigger and name it as you want to be recognizable.

![Web3 Action UI Builder](<../.gitbook/assets/image (86).png>)

The first step is setting up the **trigger type** where you can determine what type of event your action is listening to. After that, you'll be prompted to add a source code of your Web3 Action (you can see the event schema, secret and storage source code at our [GitHub repository](https://github.com/Tenderly/tenderly-actions/blob/main/packages/actions/src/actions.ts)). The next step is to set up a trigger on which event or by which schedule your function will be executed. The last step is setting up the name and a description of the Web3 Action.

### Manual Trigger

While action must specify trigger type, it doesn't have to configure a trigger. Without a configured trigger, the action will never run automatically. But you can still run your action manually! This can be useful for testing. Navigate to the specific action and click the **Manual Trigger** button.

You can provide any payload you want, as long as it matches the required schema. If your trigger type is transaction or block, you can fetch a transaction or block from a network instead of manually creating a payload.

If you deployed initialized block action, here is an example of a valid payload:

```json
{
  "network": "1",
  "blockNumber": 1000,
  "blockHash": "0x5b4590a9905fa1c9cc273f32e6dc63b4c512f0ee14edc6fa41c26b416a7b5d58"
}
```

{% hint style="success" %}
You can use a manual trigger even if the action is stopped.
{% endhint %}

[Read more about how to write a function and what runtime features are available here.](functions.md)
