---
description: >-
  Tenderly Web3 Gateway is a fast, reliable, and easy-to-scale node solution.
  Build, monitor, and improve dapp reliability and experience by using the
  tightly integrated Tenderly development platform.
---

# Intro to Web3 Gateway

## Intro to Web3 Gateway

Tenderly Web3 Gateway is a fast, reliable, and easy-to-scale node solution, giving your read-intensive dapps uninterrupted blockchain access with instantly synced data. Using Tenderly Web3 Gateway enables you to modify, consume, and analyze blockchain data, including historical data, essential to your research, analytics, and dapp-building process. Web3 Gateway is a tightly integrated part of the Tenderly development platform, giving you the right tools for building, monitoring, and improving your dapps.

The same infrastructure powering the Tenderly development platform and handling demanding read-intensive workloads is available as a plug-and-play service. This infrastructure is powered by custom and innovative architecture: we have deconstructed the monolithic general-purpose node and created a layered Web3 Gateway, providing scalability, high read throughput, and data consistency and availability by design.

The Tenderly development platform supports engineering and UX practices throughout the Web3 development lifecycle, giving you the tools you need to build, debug, test, and optimize your smart contracts. Following the go-live, Tenderly tools help you establish advanced notifications and active monitoring, aiding issue detection and troubleshooting. With Tenderly, you also improve your live production dapps in terms of user experience, interactivity, and reliability, as well as by automating business logic. Learn how the Tenderly development platform supports dapp development and UX practices.

## Guides and References

In the Tenderly Dashboard, go to Web3 Gateway. You'll see a list of supported networks, with a JSON RPC access URL for each. Use the URL to connect your dapp to a network using Web3 Gateway.

{% hint style="info" %}
The RPC URL contains your private access key. You must securely manage the URL and the access key. In case of a breach, you can regenerate the access key in the Tenderly Dashboard to protect against unauthorized access.
{% endhint %}

Here are useful guides to help you get started with Tenderly Web3 Gateway:

- [Quickstart by querying blockchain data through Web3 Gateway](quickstart-query-blockchain.md), using a visual request builder in the Tenderly Dashboard or copying the request as runnable code.
- Browse [brief reference of supported JSON RPC endpoints](brief-json-rpc.md), with examples and method invocation scripts.
- Browse [detailed reference of standard JSON RPC endpoints](detailed-json-rpc.md) supported by Web3 Gateway, drilling into the structure of request and response objects.

## Dapp development and UX practices

The Tenderly development platform supports various engineering practices throughout the dapp development workflow. It also enables you to monitor smart contract usage, detect issues, and improve dapp user experience in production.

The platform tools focus on smart contract execution, network-related aspects of development, and monitoring production dapps. Therefore, they complement other tools for building and deploying smart contracts.

Here are some dapp development practices that can benefit from Tenderly tools:

- **Developer-facing practices** make the development and refinement of smart contracts more accessible and efficient. To boost your development, make sure to:
  - Debug smart contract efficiently with decoded transactions using [Debugger](../debugger/how-to-use-tenderly-debugger/investigating-a-failed-transaction.md) .
  - Understand gas consumption by analyzing smart contracts using [Gas Profiler](debugger/how-to-use-tenderly-debugger/).
  - Troubleshoot transaction bugs efficiently by using Transaction Simulator.
  - Verify bug fix correctness and gas usage improvements using Transaction Simulator with source code editing.
  - Share smart contracts and blockchain interactions with other developers and communities using Sandbox.
- **Quality-facing practices** support the reliability of your code and the final product. To improve these practices, you can:
  - Complete integration testing using Forks hooked into your CI/CD process.
  - Stage your dapp using Forks.
- **UX-facing practices** help you create a better user experience in your dapps.
  - Dry-run transactions for the user even before the dapp sends them to the chain by using Simulation API or Forks.
  - Deliver data-rich notifications and improve interactivity by building automation with Web3 Actions.
- **Product-facing practices** enable you to improve dapp reliability and quality and inform the decision-making process.
  - Stage your dapp for exploration and manual testing with Forks.
  - Provide awareness of critical changes through granular Alerts.
  - Build core project automation with Web3 Actions.
  - Create advanced monitoring to track trends of on-chain asset values and usage with Web3 Actions.
  - Detect issues in production by building comprehensive monitoring with Web3 Actions and Alerting.
  - Observe transactions as they happen with the Transaction overview.

## Usage quota and rate-limiting

Web3 Gateway usage is rate-limited, with a monthly usage quota, expressed in **Tenderly Units (TU)**. Read, write and calculate RPC calls have different usage footprint, and thus contribute differently to the toal usage over a time-period. Find out more about [usage and rate-limiting details](pricing.md).
