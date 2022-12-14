---
description: >-
  Learn all about Tenderly Forks, an isolated development and testing
  environment. Find out how to create a Fork from the Dashboard and simulate
  complex tx scenarios without deploying to a testnet.
---

# How to Create a Fork

A **Tenderly Fork** is an isolated environment that reflects the most recent data and state of the Mainnet or any other of the 20+ networks Tenderly supports. It allows you to "duplicate" the selected network and use it for the purposes of your project, without submitting changes to the actual network. Forks expose a JSON-RPC URL, so they behave as any node would.

Forks also enable you to chain multiple Tenderly simulations, so one impacts the subsequent ones. This way, you can test complex transaction scenarios while using live on-chain data. You can even examine how certain transactions would have transpired at a specific point in the past by choosing a historical block number. &#x20;

As an environment for running simulations, Forks allow you to control every aspect of that environment using [customization APIs](../simulation-api/tenderly-fork-customization-via-api/), from simulated balances in wallets to the passage of time.

There are several ways to work with Tenderly Forks:

* Create a Fork and perform simulations using the Dashboard (covered in this guide)
* Explore the [programmatic approach to creating Forks](https://docs.tenderly.co/simulations-and-forks/simulation-api#2-create-a-fork-environment), using them with Ethers to [perform simulations](sending-transactions-to-forks.md), and different ways to [integrate forks in your project](https://docs.tenderly.co/simulations-and-forks/simulation-api#2-create-a-fork-environment).

## Working with Forks using the Dashboard

Let's start up a new Fork:

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 10.22.04.png>)

Choose the network you want to fork and name it:

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 10.23.08.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 10.24.00.png>)

You can choose the block from which you want to fork the chosen network, either latest or historical ([**read more about that here**](../how-to-simulate-a-transaction/pending-vs-historical-block.md)):

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 10.25.01.png>)

Regardless of the chosen block, we can now create a simulation on our newly created Fork:

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 10.27.32.png>)

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.46.59.png>)

You can use either public or [**custom contracts**](../how-to-simulate-a-transaction/transaction-parameters.md) here as well:

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.47.27.png>)

All that is left to do is fill out the fork simulation parameters, click **Simulate Transaction** and that's it - you can now run as many simulations as you want on your fork!

#### A few important notes to be aware of when using Tenderly Forks:

{% hint style="warning" %}
When you are creating a **Fork** from the **block number N**, the **Simulations** you run on that Fork **will run in block number N and not N + 1**.&#x20;

This means that your Fork, when created, has all the states up to and including block number N-1, and not N.
{% endhint %}

{% hint style="info" %}
Each **Simulation** you do on your **Fork** going forwards will be placed in a separate block, regardless of using the [**Historical** or the **Pending block**](../how-to-simulate-a-transaction/pending-vs-historical-block.md) option.
{% endhint %}

{% hint style="success" %}
**Fork Parents** are a feature that allows for greater control over [**Simulations**](../how-to-simulate-a-transaction/) you run on your **Forks**, and much easier repeated testing of specific (historical) scenarios on your forked networks. [**Read more about Fork Parents here.**](fork-parents.md)****
{% endhint %}



An unrelated but still useful note:

{% hint style="success" %}
Tenderly now automatically simulates the (expected) outcome of pending transactions when you paste the tx hash into the search bar, both in your [**Dashboard**](https://dashboard.tenderly.co/) and in our [**Public Explorer**](https://dashboard.tenderly.co/explorer).

This feature is available to all users, even if they are not logged in. That means that **you can now simulate live pending transactions** in this way even [**from our Explorer page**](https://dashboard.tenderly.co/explorer) without having an account - but you really should make one (it's free) so you can use the full power of our [**Simulations**](../how-to-simulate-a-transaction/) **** and **Forks** 🚀

Read more about it [**here**](../../monitoring/contracts/mempool-and-simulating-pending-transactions.md).
{% endhint %}
