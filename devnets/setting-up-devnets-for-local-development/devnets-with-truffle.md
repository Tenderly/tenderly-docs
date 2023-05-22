# DevNets with Truffle

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
