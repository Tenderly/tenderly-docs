---
description: >-
  Learn more about Transaction Simulator and how you can use it for development,
  testing, improving dapp UX, and more. Explore four Tenderly simulation
  methods: UI, RPC, API, and Forks.
---

# Intro to Simulations

Transaction Simulator allows you to see a transaction’s execution without sending it to the blockchain. It gives you the results of running a transaction against any point in blockchain history, including the latest block.&#x20;

With Transaction Simulator, your transactions are run in a lightweight simulation environment, delivering detailed information about state changes, emitted events (logs), gas usage, and all calls that a simulated transaction made.&#x20;

You can then use this information for smart contract development purposes or to influence the decision-making process for your dapp code. You can also provide such information to your end users and empower them to confidently use your dapp.

{% hint style="info" %}
Tenderly simulates unsigned transactions, so you don’t necessarily need to own an account’s private key to simulate transactions from a sender.
{% endhint %}

### 4 Ways to use Transaction Simulator

You can simulate transactions in four ways:

1. **Simulation UI**: This guided approach provides an IDE-like experience for running simulations. Use this option if you’re using Transaction Simulator for the first time and want to follow a step-by-step flow. \
   \
   Use Simulation UI when you want to troubleshoot or test the behavior of your smart contracts, verify gas optimization fixes, and see how any transaction would execute with different parameters. To get started, follow this [Simulation UI Quickstart](how-to-simulate-a-transaction/).
2. **Tenderly Web3 Gateway’s Simulation RPC**: This option gives you blockchain access with the ability to simulate transactions before sending them on-chain. \
   \
   You can use it in your dapp so your users can simulate and send transactions relying on the same RPC. Follow this [Simulation RPC Quickstart](simulation-rpc.md) to introduce it to your project.
3. **Simulation API**: With this approach, you can integrate Transaction Simulator into your dapp code using REST endpoints. This method allows you to get certain advanced responses such as gas estimations for simulated transactions. \
   \
   You can use Simulation API to both streamline your development process and improve the end-user experience in your dapp. Check out the [Simulation API Quickstart](simulation-api/) to start the integration.&#x20;
4. **Forks**: Forks are on-demand stateful simulated networks accessible through the Ethereum JSON-RPC interface. A Fork also enables you to run a staging environment for your dapp so you can onboard your users gas-free. \
   \
   You can run simulations on a private Fork for development and testing purposes. Start by going through the [Simulation Fork Quickstart](broken-reference).

{% hint style="info" %}
Using Simulation API and Forks allows you to persist simulation data on Tenderly so you can revisit it at any time or expose it to your dapp users. \
\
When using Simulation RPC, simulations are not persisted.
{% endhint %}



To choose between these two modes, use the `simulation_type` parameter.

### Single simulations and simulation bundles

In the simplest form, you can use Simulation RPC and Simulation API to simulate individual transactions in a “simulate-and-forget” manner. However, you might want to simulate a sequence of interdependent transactions. You can achieve this using simulation bundles.

For example, if you want to simulate an ERC-20 transferFrom transaction, the spender first needs to be approved. Two transactions are needed for this scenario:

1. Approve the spender
2. Simulate the spender’s transferFrom from the sender’s ERC-20 balance

There are two ways to simulate the two chained transactions:

* **Bundle simulations** by sending an array of transactions. These transactions will get simulated one after the other using [Simulation Bundle RPC](simulation-rpc.md#example-simulate-a-mint-approve-transfer-sequence) or [Simulation Bundle API](broken-reference). In both cases, the transactions are simulated as if they were consecutively sent to a network.
* **Use a Fork** and send transactions consecutively through the Fork’s RPC interface.

For more information, see this example on [using simulation bundles](simulation-api/bundled-simulations.md).

### Using Transaction Simulator

Transaction Simulator allows you to run on-chain smart contracts off-chain, relying on the current or historical state of the blockchain. Since an off-chain execution runs in Tenderly’s isolated environment, you have a high level of control over the simulation context.&#x20;

For instance, you can run a simple transaction on the latest block with real-time blockchain data. You can also deliberately run a transaction on a historical block, specify a particular state value for the involved smart contracts, override block header fields, or even run an alternative version of smart contract code.&#x20;

In other words, with simulations, you can do anything from simply running a smart contract at the latest blockchain state to running it in an alternate, hypothetical timeline.

Transaction Simulator offers invaluable benefits during development and in production:

1. **Improving smart contract development, debugging, and testing**: You can use Transaction Simulator to run and debug custom transactions, just like the “Run locally” button in your IDE used to do. This enables you to preview transaction outcomes prior to deployment, detect and debug errors, and ensure your code executes as expected once deployed.&#x20;
2. **Optimizing the usage of mainnet dapps**: By enabling a preview of a transaction’s execution, effects, and final outcome, your dapp code or users can make an informed decision depending on whether a transaction is beneficial or not. This way, you can find optimal transaction inputs to maximize its value.
3. **Bringing more visibility into tx outcomes before signing**: For instance, allowing your users to simulate transactions from your wallet brings a higher level of security. Consequently, this improves dapp user experience. You can also use simulations in your governance process, to preview the voting results and proposal impacts, and more.&#x20;
4. **Ensuring dapp reliability by avoiding unexpected failures**: Preview transaction outcomes to eliminate either unsuccessful (reverted) transactions or successfully executed transactions with unwanted results from your dapp.

Here are possible ways you can use Transaction Simulator in your project:

#### Smart contract development and testing

As a smart contract engineer, you can use simulations to enhance your development process. Here are some practices that can help you get started:&#x20;

* **Troubleshoot smart contracts with the Simulation UI and Debugger.** Once you simulate a contract’s execution, you can use Debugger to identify and fix issues should they occur.  Then, simulate transactions running on the bugfixed code to verify the fix.
* **Verify gas optimization fixes with the Simulation UI and Gas Profiler.** Identify gas-intensive lines of code and optimize them to reduce smart contract gas usage. Next, check whether your fixes are effective using Simulation UI.&#x20;
* **Test the behavior of your smart contracts with the Simulation UI** under different circumstances. It allows you to override contract state variables, block number, timestamp, sender, value, and so on.
* **Streamline smart contract tests by integrating a Fork** within a Hardhat project as a testing network. This way, you have your own private testing network where you can simulate different scenarios and troubleshoot, track, and debug failing tests.

For more information, explore:

* [How to troubleshoot transactions](http://md2doc-split/tutorials/troubleshooting-transactions.md) to recover from a failure.
* [How to debug a smart contract](http://md2doc-split/tutorials/debugging-smart-contracts.md) to find the cause of an issue and verify the fix.

#### Dapp staging and testing

Transaction Simulator allows you to stage dapps for frontend builders, testing, and user onboarding. You can:&#x20;

* **Integrate Staging Forks** to stage your dapp to onboard users without spending any gas. With a Fork, you get the full behavior of a test network and fast transaction execution, which makes onboarding fast.
* **Integrate Development Forks** to stage your smart contracts for frontend developers. This integration provides them with instantaneous transaction execution so they can easily stress-test your dapp.
* **Integrate Testing Forks** to stage your dapp for efficient manual or automated end-to-end testing, aiding your team's quality assurance practices.

#### Dapp user experience and reliability

You can also use Transaction Simulator to ensure the reliability of your dapp and give a better dapp experience to your users. By using different simulation methods, you can bring insight into transaction execution to your code or your end-users. &#x20;

You can do this in the following way: &#x20;

* Integrate Simulation API or Simulation RPC so your code can **make recommendations to dapp users and prevent potential mishaps** by avoiding failed transactions or suboptimal results.
* Integrate Simulation API or Simulation RPC to **improve dapp UX by providing dapp users with higher visibility into transaction outcomes**. This way, your users can avoid paying gas for reverted transactions and eject from sending transactions with suboptimal or undesired outcomes.
* Integrate with Staging Forks to **run your dapp in demo mode**. This way, you can easily onboard new users to your dapp and allow them to try it out safely and gas-free. They can preview your dapp’s functionalities and get familiar with the interface without any risks so they can start using your mainnet dapp confidently.
* Use the Simulation UI to **verify optimal transaction parameters and avoid failures** before sending transactions to mainnet dapps.
* Use the Simulation UI and Debugger to **troubleshoot failed transactions** sent to different types of mainnet dapps such as DeFi applications. This way, you can improve and speed up your issue resolution process, further boosting end users' satisfaction.&#x20;

#### Strategy validation

Running simulations gives you a preview of important actions, governance proposals, and protocol changes before committing them to the blockchain. Different simulation methods allow you to:

* Run simulation bundles via Simulation API to validate a sequence of transactions, such as those made up of approvals and swaps for DeFi products.
* **Improve governance practices** by simulating proposals on Forks and seeing how they work before applying them.
* Integrate Simulation API or Simulation RPC to inform the strategies you programmed into your dapp.

#### Research and hack analysis

Play around with smart contracts.

* Use Simulation UI or Simulation API to

\
