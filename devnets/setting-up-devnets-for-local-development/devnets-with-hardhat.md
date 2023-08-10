# DevNets with Hardhat

Hardhat is an Ethereum development environment that simplifies smart contract development, testing, and deployment.

### Manual RPC URL creation via Spawn DevNet

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

Replace **`YOUR_DEVNET_JSON_RPC_URL`** with the DevNet RPC URL, you obtained from Tenderly by [Spawning a DevNet via UI](https://dashboard.tenderly.co/nenad/tst/devnets).

### Automatic creation of RPC URL

One alternative is to utilize the `spawn-rpc` CLI command, which enables the automated process of spinning up a DevNet and injecting it directly into your HardHat config file.

{% hint style="info" %}
Each time the `spawn-rpc` the command is called, a new RPC URL will be generated from a fresh state of the specified network based on template.
{% endhint %}

```bash
brew tap tenderly/tenderly && brew install tenderly
tenderly login

tenderly devnet spawn-rpc --project <YOUR_PROJECT_SLUG> --template <YOUR_TEMPALATE_SLUG>
# prompts active devnet RPC URL
```

See an example of how you to [integrate CLI into your project](https://github.com/Tenderly/devnet-examples/tree/main/CI-project).

{% content-ref url="../advanced/automated-devnet-spawning-bash-and-javascript.md" %}
[automated-devnet-spawning-bash-and-javascript.md](../advanced/automated-devnet-spawning-bash-and-javascript.md)
{% endcontent-ref %}
