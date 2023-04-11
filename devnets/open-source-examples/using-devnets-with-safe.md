---
description: Learn how to integrate DevNets in a Safe project.
---

# Using DevNets With Safe

Safe is a multi-signature wallet on the Ethereum blockchain that provides secure and flexible management of digital assets. It allows customizable access controls, multiple signatures for transactions, and seamless integration with decentralized finance (DeFi) applications, making it a popular choice for projects and organizations.

To integrate DevNet for the Safe project, follow these steps:

1. Clone the [Safe contracts repository](https://github.com/safe-global/safe-contracts):

```bash
git clone git@github.com:safe-global/safe-contracts.git
cd safe-contracts
```

2. Install dependencies:

```bash
yarn install
```

3. Safe contracts use Hardhat as its development tool. Configure **`hardhat.config.js`** to use the DevNet JSON-RPC URL:

```tsx
require("@nomiclabs/hardhat-ethers");
// ... other imports ...

const DEVNET_RPC_URL = "YOUR_DEVNET_JSON_RPC_URL";

module.exports = {
  solidity: "0.7.6",
  networks: {
    devnet: {
        ...sharedNetworkConfig,
        url: DEVNET_RPC_URL,
     },
    // ... other network configurations ...
  },
  // ... other configurations ...
};

```

Replace **`DEVNET_RPC_URL`** with the DevNets JSON-RPC URL you obtained from Tenderly.

4. Now you can run tests using the DevNet network:

```
npx hardhat test --network devnet
```

By integrating DevNet, you can deploy and test in an isolated environment, helping you ensure that the contracts work as expected without interfering with other test environments and with consistent mainnet data.

Additionally, you can automate this process with the Tenderly CLI. See the [code example here](https://github.com/Tenderly/devnet-examples/tree/main/CI-project).
