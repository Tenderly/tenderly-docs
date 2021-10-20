# Execution Overview

![](<../../.gitbook/assets/image (57).png>)

Execution Overview - think of it as the bird's-eye view of the transaction. At a glance, you can see the exact code paths of all of the Smart Contracts that participated in a given transaction. You can open the transaction from the image above by [clicking here](https://dashboard.tenderly.co/tx/main/0x97c37f37988c010a37a8c550b03af37c04bffa2ba6be7d1135f0a26c0e00f532).

When you click on a function name, you can see the context in which that function was called:

![](<../../.gitbook/assets/image (30).png>)

But let's say you want to dig deeper. You can do that by clicking the [**View in Debugger**](../../debugger/how-to-use-tenderly-debugger/) button next to the function name.

### Contracts

When you are in the **Transaction Overview** tab, in the upper navigation you can click on **Contracts** (or **Addresses**) in order to see all of the contracts that have been involved in a certain transaction:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 15.21.21.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 15.21.39.png>)

### Events

Smart Contract Events are the de-facto way of notifying interested parties that some event has occurred. The Logs themselves also contain valuable information in addition to the information that a particular event has occurred.

![](<../../.gitbook/assets/image (55).png>)

When we open the **Events/Logs** tool, we can see all of the Logs that were [emitted during a transaction](https://dashboard.tenderly.co/tx/main/0x97c37f37988c010a37a8c550b03af37c04bffa2ba6be7d1135f0a26c0e00f532/logs). What is even better is that **the event parameters are already decoded and shown in a human-readable format**. No more time wasted decoding hex strings to see what happened. You can also filter the Events by name and Smart Contract. Time: saved!

### State Changes

As Smart Contracts are getting more and more complex, the states of those smart contracts are getting more complex as well.

![](<../../.gitbook/assets/image (39).png>)

Here we see that not only does Tenderly show the state variables that were changed, but also **all of them are decoded for your convenience**. **And yes, structures are decoded correctly as well**.

The image above shows the moment when MakerDAO Debt Ceiling raise was passed. You can see that transaction and it's [intricacies here](https://dashboard.tenderly.co/tx/main/0x8ab00efe4d4626eabd6752a6d9f130ab95773a2be312027c0f3776685ffb9ffa).

### Stack Traces (Debugger)

Stack traces are a very import part of any developer's workflow both locally, but in production as well. That's why Stack traces [were one of the first features](http://blog.tenderly.co/improving-smart-contract-development-with-tenderly-and-human-readable-stack-traces/) we released, first as a [CLI tool](https://github.com/Tenderly/tenderly-cli) and later as part of our platform.

![](<../../.gitbook/assets/image (50).png>)

[**The stack trace above**](https://dashboard.tenderly.co/tx/main/0x66016977d78e01a8ff0609f14ec6fc8caf95db6c666e86ac589bd76942688db0)** shows the exact line of code where the transaction failed**. From there, you can click **Debug Error** and find the issue in no time! How convenient!

### Gas Profiler

![](<../../.gitbook/assets/image (54).png>)

The chart you see in the image above is called a flame graph. It is a common way to show usage of a resource like a CPU. The example above is a Kyber Network transaction, [which you can find here](https://dashboard.tenderly.co/tx/main/0x97c37f37988c010a37a8c550b03af37c04bffa2ba6be7d1135f0a26c0e00f532/gas-usage).

Each line shows the sum cost of the lines beneath it. If you click on any of the lines (functions), you can see a detailed breakdown of the gas cost of the functions that were invoked.

![](<../../.gitbook/assets/image (42).png>)

You can finally see which functions are using the most gas and pick the right parts of your code to optimize.
