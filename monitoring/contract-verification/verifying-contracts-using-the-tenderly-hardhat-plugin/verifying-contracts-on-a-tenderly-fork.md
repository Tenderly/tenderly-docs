# Verifying Contracts on a Tenderly Fork

You can deploy Smart Contracts to Forks and send transactions to those contracts later on. To use Tenderly tools for the transactions simulated on a Fork, it’s necessary to verify the contracts. The process of verification on a Fork doesn’t differ much from verifying contracts on public networks.

{% hint style="info" %}
Keep in mind that the contracts verified on a Fork are valid only within the context of the Fork, so there’s no concept of private or public verification on a Fork.
{% endhint %}

## Add a Tenderly Fork as a network to the Hardhat configuration

Next, you need to further configure the Hardhat and Tenderly plugin when verifying a contract on a Fork. The additional configuration will specify the Tenderly Fork as a network so Ethers can use it for blockchain operations at a later point.

Follow this guide to obtain [Fork JSON-RPC URL](https://docs.tenderly.co/simulations-and-forks/how-to-create-a-fork/how-to-get-a-fork-json-rpc-url-and-id) from the dashboard.

To achieve this, add the following `tenderly` property of `networks` to the Hardhat config:

```diff
// File: hardhat.config.ts
// --snip--
const config: HardhatUserConfig = {
  solidity: "0.8.9",
  networks: {
    --snip--
+  tenderly: {
+     chainId: 5582,
+     url: "https://rpc.tenderly.co/fork/2aeae177-a3e8-492f-9861-1c9aa8856235",
+   },
    --snip--
  }
};

export default config;
```

Here’s an overview of the configuration parameters used in the example above:

| Property | Description                                                                                                                                                                                                                                                        |
| -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| chainId  | The [chain ID](https://consensys.net/docs/goquorum/en/latest/concepts/network-and-chain-id/) you associate to the Fork. Use an arbitrary number, different from usual network IDs. This is to ensure that you are not vulnerable to the transaction replay attack. |
| url      | The JSON-RPC URL of your Fork. You can get it from the Fork page in the Dashboard. It follows the structure `https://rpc.tenderly.co/fork/{forkId}`, where forkId is a unique UUID identifier of the Tenderly Fork.                                                |

## Automatic & simple manual verification on a Tenderly Fork

Both automatic and simple manual verification run automatically if the configuration is accurate. You don’t need to make any adjustments to the deployment code.

**Note**: You need to pass `--network tenderly` so Hardhat uses your Fork as a network.

Use the following script to run this type of deployment and verification:

```bash
# Runs automatic verification

hardhat run scripts/greeter/automatic.ts --network tenderly

# Runs manual simple

hardhat run scripts/greeter/manual-simple.ts --network tenderly
```

Next, go back to your Fork in the Tenderly Dashboard. You should see a “Contract Creation” transaction, corresponding to the contract deployment. Click “Contracts” and you should see that the Greeter contract is verified.

![Contract Creation Transaction in Tenderly Fork](<../../../.gitbook/assets/fork transactions>)

## Advanced manual verification on a Tenderly Fork

The advanced manual verification of contracts on a Fork is analogous to the advanced manual verification on a public network, with a few additional settings.

**The key difference**: You have to use `tenderly.verifyForkApi` instead of `tenderly.verifyApi`. .

**Note**: You can verify a contract you previously deployed on a Fork. The verification requires only the address of the deployed contract.

Here’s a script that deploys the Greeter contract on a Tenderly Fork and verifies it immediately.

```typescript
// File: scripts/greeter/manual-advanced-fork.ts
import { readFileSync } from "fs";
import { ethers, tenderly } from "hardhat";
import * as dotenv from "dotenv";

dotenv.config();

const FORK_ID = process.env.TENDERLY_FORK_ID || "";

export async function main() {
  const Greeter = await ethers.getContractFactory("Greeter");
  const greeter = await Greeter.deploy("Hello, Manual Hardhat on Fork !");

  await greeter.deployed();
  const greeterAddress = greeter.address;
  console.log("Manual Advanced (fork): {Greeter} deployed to", greeterAddress);

  tenderly.verifyForkAPI(
    {
      config: {
        compiler_version: "0.8.9",
        evm_version: "default",
        optimizations_count: 200,
        optimizations_used: false,
      },
      root: "",
      contracts: [
        {
          contractName: "Greeter",
          source: readFileSync("contracts/Greeter.sol", "utf-8").toString(),
          sourcePath: "contracts/whatever/Greeter.sol",
          networks: {
            // important: key is the Fork ID (UUID-like string)
            [FORK_ID]: {
              address: greeterAddress,
              links: {},
            },
          },
        },
        {
          contractName: "console",
          source: readFileSync(
            "node_modules/hardhat/console.sol",
            "utf-8"
          ).toString(),
          sourcePath: "hardhat/console.sol",
          networks: {},
          compiler: {
            name: "solc",
            version: "0.8.9",
          },
        },
      ],
    },
    process.env.TENDERLY_PROJECT || "",
    process.env.TENDERLY_USERNAME || "",
    FORK_ID
  );
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

{% hint style="info" %}
**Note**: In the `networks` segment of the configuration, we used [computed property names](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object\_initializer#computed\_property\_names), so the value of `FORK_ID` becomes a property in the `networks` object.
{% endhint %}

To execute this script, place the proper values for `TENDERLY_PROJECT`, `TENDERLY_USERNAME`, and `TENDERLY_FORK_ID`.

```bash
TENDERLY_PRIVATE_VERIFICATION=true \
TENDERLY_PROJECT=myProject \
TENDERLY_USERNAME=myUsername \
TENDERLY_FORK_ID=2aeae177-... \
npx hardhat run scripts/greeter/manual-advanced-fork.ts --network tenderly
```

If you’re keeping these values in an externalized configuration using the `dotenv` package, place `TENDERLY_PROJECT`, `TENDERLY_USERNAME`, and `TENDERLY_FORK_ID` in the `.env` file. This simplifies the command to:

```bash
TENDERLY_PRIVATE_VERIFICATION=true \
npx hardhat run scripts/greeter/manual-advanced-fork.ts --network tenderly
```

Here’s a summary of the arguments of `verifyForkAPI`:

| Parameter           | Description                                                                                                                                                     |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| verificationRequest | A specification of the config, root, and contracts                                                                                                              |
| username            | Your username                                                                                                                                                   |
| projectSlug         | The slug of the project enclosing the Fork                                                                                                                      |
| forkId              | The Fork ID: a unique UUID identifier of the Tenderly Fork. You can find it in the JSON-RPC URL shown in the Dashboard (https://rpc.tenderly.co/fork/{forkId}). |

### Configuring `verificationRequest`

The `verificationRequest` consists of the following parts:

* The **config** refers to the [Solidity compiler configuration](https://docs.tenderly.co/monitoring/contract-verification/verifying-contracts-using-the-tenderly-hardhat-plugin/manual-contract-verification#the-solidity-compiler-config).
* The **root** is set to an empty string (`root: ""`) so the contract is verified for the entire Fork. To make a contract valid starting with a particular Simulated transaction in the Fork, set it to the Simulation ID (UUID assigned by Tenderly).
* The **contracts** entail a list of **contracts and libraries** you’re verifying. For more details, see the [reference for _contracts_ verification property](https://docs.tenderly.co/monitoring/contract-verification/verifying-contracts-using-the-tenderly-hardhat-plugin/manual-contract-verification#the-solidity-compiler-config).

The `contracts` property is a list of all the contracts you’re verifying and the libraries they’re using. The main difference is that the key of each entry in the `networks` property has to be the Fork ID, like on the line 8 in the listing below:

```typescript
// --snip--
{
   contractName: "Greeter",
   source: readFileSync("contracts/Greeter.sol", "utf-8").toString(),
   sourcePath: "contracts/whatever/Greeter.sol",
   networks: {
     // important: key is the Fork ID (UUID-like string)
     [FORK_ID]: { // using ES6 computed properties
         address: greeterAddress,
         links: {},
     },
   },
},
// --snip–
```
