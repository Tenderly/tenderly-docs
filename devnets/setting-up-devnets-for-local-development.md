---
description: Learn how to use DevNets as part of your local development workflows.
---

# Setting Up DevNets for Local Development

In this guide, you'll learn how to set up DevNets for local development in a HardHat, Foundry, and Truffle project.&#x20;

### Why use DevNets in your local development workflows?

1. **Faster development and testing**: Quickly test and debug smart contracts without the latency of public testnets or Mainnet and accelerate your development and debugging.
2. **Customization of the network state**: You get full control over the network, including the state, block number, account balances, timestamp, etc. This allows you to customize the environment to match your project requirements.
3. **Privacy and security**: Your smart contracts and sensitive data remain private during development and testing. This can be particularly important if you are working on proprietary projects or handling sensitive user data that should not be exposed on public networks.
4. **Independence from public testnets**: Acquiring ETH on testnets can be a tedious and time-consuming process, often requiring you to use faucets or request tokens from others. DevNet eliminates this issue by providing a seamless way to add funds to your account. Additionally, it allows for faster transaction execution, enabling you to test and iterate on your smart contracts more efficiently.
5. **Integration with development tools**: A local DevNet is integrated with Tenderly's development toolset, such as Debugger and Gas Profiler. Seamless integration can streamline your development workflow, enabling you to work more efficiently and boost productivity.

### Prerequisites

Before setting up a DevNet locally, ensure you have completed the following steps:

1. **Create a Tenderly account:** If you haven't already, [sign up for Tenderly to access DevNets](https://dashboard.tenderly.co/register?redirectTo=devnets).
2. **Set up a DevNet template:** After creating your account, configure a DevNet Template to match your project's requirements.

{% hint style="info" %}
If you haven't completed these steps, please visit this page for guidance on [creating a DevNet template](intro-to-devnets.md#basic-devnet-usage).&#x20;
{% endhint %}

### Setting up a DevNet for a **Hardhat project**

Hardhat is an Ethereum development environment that simplifies smart contract development, testing, and deployment.

To set up DevNet with Hardhat, follow these steps:

1. Install Hardhat if you haven't already:

```bash
yarn add --dev hardhat
```

2. Create a **`hardhat.config.js`** file in your project directory and configure it to use the DevNet JSON-RPC URL that you have copied from DevNets.

```bash
module.exports = {
  networks: {
    devnet: {
      url: "YOUR_DEVNET_JSON_RPC_URL",
			chainId: 1,
    }
  }
};
```

Replace **`YOUR_DEVNET_JSON_RPC_URL`** with the DevNet RPC URL you obtained from Tenderly.

One alternative is to utilize the `spawnRPC` CLI command, which enables the automated process of spinning up a DevNet and injecting it directly into your HardHat config file.

{% hint style="info" %}
Each time the `spawn-rpc` command is called, a new RPC URL will be generated from a fresh state of the specified network.
{% endhint %}

```bash
brew tap tenderly/tenderly && brew install tenderly
tenderly login

tenderly devnet spawn-rpc --project <YOUR_PROJECT_SLUG> --template <YOUR_TEMPALATE_SLUG>
# prompts active devnet rpc url
```

See an example of how you to [integrate CLI into your project](https://github.com/Tenderly/devnet-examples/tree/main/CI-project).

### Setting up DevNet for a Foundry **project**

Foundry is a Rust-based Ethereum smart contract development framework that provides an easy-to-use CLI for developers.

Make sure you have everything installed first:

* [Install Rust](https://www.rust-lang.org/tools/install)
* [Install Foundry](https://github.com/gakonst/foundry/)

To set up a DevNet with Foundry, follow these steps:

1. Initialize a dummy Foundry project.

```bash
forge init
```

2. Use the `forge create` command to deploy your smart contracts.

```bash
forge create --rpc-url=$(tenderly devnet spawnRPC --template <YOUR_TEMPALATE_SLUG> --project <YOUR_PROJECT_SLUG>) ./src/Counter.sol:Counter --unlocked --from 0x0000000000000000000000000000000000000000
```

### Setting up DevNet for a Truffle **project**

Truffle is a popular Ethereum development framework that simplifies smart contract development, testing, and deployment.

To set up DevNet with Truffle, follow these steps:

1. Install Truffle if you haven't already:

```bash
npm install -g truffle
```

2. Create a **`truffle-config.js`** file in your project directory and configure it to use the DevNet JSON-RPC URL:

```tsx
module.exports = {
  networks: {
    devnet: {
      host: "YOUR_DEVNET_JSON_RPC_URL",
      network_id: "*",
      gas: 4700000,
      gasPrice: 20000000000,
      from: "YOUR_ETHEREUM_ADDRESS"
    }
  }
};
```

Replace **`YOUR_DEVNET_JSON_RPC_URL`** with the DevNet RPC URL you obtained from Tenderly and **`YOUR_ETHEREUM_ADDRESS`** with your Ethereum account's address.

To streamline DevNet spawning, you can use the [Tenderly CLI](https://github.com/Tenderly/tenderly-cli).

```tsx
module.exports = {
  networks: {
    devnet: {
      host: $(tenderly devnet spawn --template=my-devnet),
      network_id: "*",
      gas: 4700000,
      gasPrice: 20000000000,
      from: "YOUR_ETHEREUM_ADDRESS"
    }
  }
};
```

Check out the entire [example project using Truffle](https://github.com/Tenderly/devnet-examples/tree/main/local-development/truffle-setup).

#### **Need further guidance?**

If you're unsure about the DevNet setup process, check out [this GitHub project](https://github.com/Tenderly/devnet-examples). It contains examples of DevNet configurations for each framework mentioned in this guide.
