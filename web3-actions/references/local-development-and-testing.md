---
description: >-
  Learn how to achieve shorter iteration times on your Web3 Action function
  code. Find out how to write automated tests for your Web3 Action functions by
  using @tenderly/actions-test.
---

# Local Development and Testing

To facilitate local development of your Web3 Action code, you can use the **@tenderly/actions-test** package (contained in tenderly-actions). It exposes a Tenderly runtime, so you can execute and perhaps test your Web3 Action in your local environment.

Install the [**@tenderly/actions-test**](https://github.com/Tenderly/tenderly-actions/tree/main/packages/actions-test) package to test your Web3 Action functions locally.

```bash
yarn add --dev @tenderly/actions-test
```

{% hint style="info" %}
It’s recommended to keep tests and run scripts for web3-actions outside of the _actions root_ directory to avoid increasing the size of your Web3 Action project.
{% endhint %}

You can use **@tenderly/actions-test** in two ways to support your development process:

* Use it within your automated tests (**recommended**).
* Create a run script in JavaScript/TypeScript.

### Using @tenderly/actions-test in your tests

To use **@tenderly/actions-test** in your tests, no additional steps are needed. Import `TestRuntime` and events you need to test your Web3 Action and assert the results.

The following examples show how to use the package to invoke the Web3 Action and pass the event object the Action functions expect.

### A working example

Check out the multisig wallet example and the way it uses **@tenderly/actions-test** to run the action function locally.

****[**Multisig wallet and running action function locally**](https://github.com/Tenderly/examples-web3-actions/tree/main/multisig-wallet#2-run-it-locally)****

### Example: running an Action function within a script

The following example shows a file at **src/web3-actions-local/run.ts** that runs three actions, passing adequate events. Note the Web3 Actions source file (`src/actions/awesomeActions.ts`) is in a sibling to directory containing the script:

**Step 1: write the run script**

```tsx
// File: src/web3-actions-local/run.ts
// web3-actions sources location: src/actions/awesomeActions.ts

import { TestPeriodicEvent, TestRuntime } from "@tenderly/actions-test";
import { everyDay, onTxEvent, whenDappPosts } from "../actions/awesomeActions";

/*
 * Running Web3 Actions code locally.
 * TestRuntime is a helper class that allows you to run the functions,
 * and set storage and secrets before running the function
 **/
const main = async () => {
  const testRuntime = new TestRuntime();

  testRuntime.context.secrets.put(
    "multisig.DISCORD_URL",
    process.env.DISCORD_URL || ""
  );

  await testRuntime.execute(everyDay, new TestPeriodicEvent());

  await testRuntime.execute(
    whenDappPosts,
    new TestWebhookEvent({ foo: "bar" })
  );

  const te = new TestTransactionEvent();
  te.to = "0x1a22...";
  te.from = "0xc023...";

  await testRuntime.execute(onTxEvent, new TransactionEvent());
};

(async () => await main())();
```

**Step 2: Extend scripts in package.json of the enclosing project**. You can add this script to your **package.json** file.

```diff
{
    ...
  "scripts": {
    ...
+   "local-w3a-run": "ts-node src/web3-actions-local/run.ts"
    ...
  }
  ...
}
```

**Step 3: Run the script**

```bash
yarn local-w3a-run
```
