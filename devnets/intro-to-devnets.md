---
description: DevNets are a managed, zero-setup environment for smart contract development.
---

# Intro to DevNets

Development Networks or DevNets is a zero-setup, managed development environment for developing, testing, and debugging smart contracts. With built-in debugging tools, DevNets eliminate the need to run any third-party software or to set up an environment.

DevNets make it easy to deploy, test, and integrate smart contacts on the latest network state as if on the public network. You get access to the latest network state without the performance delays often found in public testnets. Furthermore, your DevNets are private but allow you to control who has access from your team.

{% embed url="https://youtu.be/le4QoALNBHs" %}

### Benefits of developing on DevNets

* **Zero-setup**: Get instant access to a production node without any rate-limiting.
* **Isolated environment**: Running tests in isolation prevents interference between executions.
* **Focused on developers:** Inspect and debug transactions down to the very last OP Code and JSON-RPC call.
* **Highly flexible network**: Easily send transactions from any account, change any contract variable values, or edit the contract’s source code.
* **Unlimited faucet**: Instantly top-up the balances on your accounts and run transactions regardless of how big they are.
* **Reusable templates:** Spin up a new network with a consistently fresh state without the hassle of manually configuring the network from scratch.

### How DevNets work: Quick overview

* New blocks are mined for every new transaction that has been executed.
* Custom RPC calls enable you to change blocks, timestamps, states, contracts code, etc.
* DevNets run on Tenderly’s custom implementation of the Ethereum Virtual Machine, providing a consistent experience across the entire platform.
* We ensure that the environment has a clean state for each new DevNet by automatically cleaning up the state from previous use.
* Create templates and use the Tenderly CLI to automate the creation of environments.
* Each DevNet is created with the latest state of the chain or any other state in its history that you choose.
* Transactions are executed significantly faster compared to public testnets.

### Basic DevNet usage

{% hint style="info" %}
To spin up a DevNet, you need to have a Tenderly account. Log in or [create one here](https://dashboard.tenderly.co/register?redirectTo=devnets).
{% endhint %}

From the lefthand menu, **navigate to DevNets** and click on **Create Template**.

<figure><img src="../.gitbook/assets/devnets main screen.png" alt=""><figcaption></figcaption></figure>

When prompted:

1. **Choose the network** you want to work with.
2. **Set the block number** from network history (default: latest).
3. Give your DevNet a **unique name**.

Click **Save** to create a template.

<figure><img src="../.gitbook/assets/devnets config.png" alt=""><figcaption></figcaption></figure>

Next, click **Spawn DevNet**, and **copy the RPC URL**.

<figure><img src="../.gitbook/assets/devnets copy url (1).png" alt=""><figcaption></figcaption></figure>

You can run the following cURL command from the terminal to test if the RPC URL of your DevNet is working properly.

```bash
curl <YOUR_DEVNET_RPC_URL> -X POST -H "Content-Type: application/json" -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":0}'
```

#### Next steps:

* [How to use DevNets in local development](setting-up-devnets-for-local-development/)
* [How to use DevNets as part of your Continuous Integration pipeline](setting-up-devnets-for-continuous-integration.md)
