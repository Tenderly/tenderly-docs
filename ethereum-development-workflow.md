---
description: >-
  Learn how Tenderly tools support engineering practices throughout the dapp
  development lifecycle, help build better UX, and stay on top of your
  production dapps.
---

# 🌊 Ethereum Development Workflow

The all-in-one Tenderly development platform is a tightly integrated set of tools and services, supporting various engineering practices throughout the dapp development lifecycle. When you go into production, it enables you to monitor smart contract usage, detect and troubleshoot issues, and build a better dapp user experience.

With Tenderly, you have the tools you need to build, debug, test, and optimize your smart contracts during development. You can address some early aspects of development, including user experience, dapp interactivity and reliability, and business logic automation. Additionally, Tenderly tools complement other tools and frameworks for building and deploying smart contracts, helping you get the best possible outcome.&#x20;

Tenderly Node, a production-ready node solution, enables research and development (R\&D), as well as deploying and operating your smart contracts as they go live. This node also provides uninterrupted multi-region access to Ethereum networks, especially for read-heavy workloads.

Here are some dapp development practices that can benefit from Tenderly tools:

### **Development-facing practices**&#x20;

These practices make the development and refinement of smart contracts more accessible and efficient. To boost your development, make sure to:

* Debug smart contracts efficiently with decoded transactions using [Debugger](debugger/how-to-use-tenderly-debugger/investigating-a-failed-transaction.md).
* Understand gas consumption by analyzing smart contracts using [Gas Profiler](monitoring/contracts/execution-overview.md#gas-profiler).
* Troubleshoot transaction bugs efficiently by using [Transaction Simulator](simulations-and-forks/how-to-simulate-a-transaction/).
* Verify bug fix correctness and gas usage improvements using Transaction Simulator with [source code editing](simulations-and-forks/how-to-simulate-a-transaction/editing-contract-source.md).
* Share smart contracts and blockchain interactions with other developers and communities using [Sandbox](tenderly-sandbox.md).
* Deploy your smart contracts, query blockchain data, and connect your production apps to Ethereum networks by using the [Tenderly Node](broken-reference) - our node as a service.

### **Quality-facing practices**&#x20;

This group of practices fosters the reliability of your code and the final product. To improve these practices, you can:

* Test smart contract integration using[ Forks](broken-reference).
* Set up a [CI/CD pipeline](simulations-and-forks/integration-guides/ci-cd-pipeline-for-smart-contracts.md).
* [Stage your dapp](simulations-and-forks/integration-guides/instant-staging-qa-environment-for-dapps.md) for manual/end-to-end testing.

### **UX-facing practices**

To create a better user experience in your dapps, you can introduce practices that allow you to:

* Dry-run transactions for the user even before your dapp sends them to the chain by using [Simulation API](broken-reference) or Forks.
* Deliver data-rich notifications and improve interactivity by building automation with [Web3 Actions](web3-gateway/broken-reference/).
* Run your dapp in [demo/playground mode](simulations-and-forks/integration-guides/dapp-playground-mode.md) so your users can try it out in an isolated environment.

### **Product-facing practices**

Practices supporting your product enable you to improve dapp reliability and quality and inform the decision-making process. You can:&#x20;

* Observe transactions as they happen with the [Transaction overview](monitoring/contracts/).
* Provide awareness of critical changes through granular [Alerts](web3-gateway/broken-reference/).
* [Build core project automation](web3-actions/tutorials-and-quickstarts/how-to-send-a-discord-message-about-a-new-uniswap-pool.md) with Web3 Actions.
* [Create advanced monitoring to track trends](web3-actions/tutorials-and-quickstarts/how-to-handle-on-chain-events.md) of on-chain asset values and usage with Web3 Actions.
* Detect issues in production by building comprehensive monitoring with Web3 Actions and Alerting.
