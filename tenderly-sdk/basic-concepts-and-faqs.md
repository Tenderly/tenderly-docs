---
description: >-
  Learn the basic concepts and get answers to the most common questions related
  to the Tenderly SDK.
---

# Basic Concepts & FAQs

### **What's a Tenderly project (project slug)?**

Project slugs are unique identifiers for each project you create with Tenderly. It’s automatically created from the project's name by converting it to lowercase and replacing spaces with hyphens. The SDK uses project slugs to reference and manage projects when interacting with the Tenderly API.

**Guides**

* [How to obtain the project slug/name](https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name#project-name-or-slug)

### **What's a Tenderly account (username and organization slug)?**

An account represents a user or an organization on the Tenderly platform. Each account has a unique username (for individual users) or organization slug (for organizations). The SDK uses these identifiers to specify the owner of a project, wallet, or contract when making requests to the Tenderly API.

**Guides**

* [How to obtain the account name](https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name#username)
* [How to obtain the organization name](https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name#organization-name)

### **What’s the difference between a wallet and a contract?**

**A wallet** is a user-controlled account that stores and manages digital assets like cryptocurrencies. Wallets can initiate transactions, interact with smart contracts, and receive assets.

**A contract** is a smart contract deployed on the blockchain. It contains code that executes automatically when certain conditions are met or when a transaction invokes it. While wallets are primarily used to manage assets, smart contracts are used to define the rules and logic of dapps and can interact with other contracts or wallets.

### **What's a simulation?**

A simulation is a way to test transactions, interactions, and contract executions in a controlled environment without actually executing them on-chain. By simulating transactions, you can test and validate smart contract bug fixes or code updates, replay failed transactions to identify the cause of a problem, and preview the expected outcomes.

The Tenderly SDK provides utilities for simulating individual transactions and bundled transactions from code via the API. To learn more about how Tenderly's Simulation API works, check out the [Simulation API documentation page](broken-reference).&#x20;

To better understand the impact of simulations in real-world applications, Safe and Instadapp are great examples of how simulations can be used both in development and production.&#x20;

Read the Safe and Instadapp case studies to learn more:

{% embed url="https://blog.tenderly.co/case-studies/instadapp/" %}

{% embed url="https://blog.tenderly.co/case-studies/safe/" %}

### Pricing

The pricing for the Tenderly SDK depends on the specific feature you are using. For example, if you use the Tenderly SDK to simulate transactions, simulations are priced based on how many Tenderly Units (TUs) are consumed to execute the simulation.

**Executing one simulation consumes 40 TUs.**

Below you can find links to relevant pricing sections for each Tenderly SDK namespace:

* Simulations (Pricing for [Advanced Compute methods](https://docs.tenderly.co/web3-gateway/pricing) applies)
* Wallets and Contracts ([Standard pricing for monitoring](https://tenderly.co/pricing) applies)
