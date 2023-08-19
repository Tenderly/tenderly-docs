# Manual Contract Verification

In addition to automatic verification, you can verify your Smart Contracts manually in your Hardhat deployment scripts.

Manual contract verification is applicable in the following situations:

* Your Smart Contract is already deployed on a blockchain.
* You want to have more control over verification configuration.

## Manual verification methods

You can choose between two ways to manually verify a contract, including:

* **Simple**, where a single function call completes the verification process by accepting two arguments – a contract name and a contract address.
* **Advanced**, where you need to specify arguments manually with a high level of detail, which provides more freedom and flexibility throughout the verification process.

{% hint style="success" %}
**Turn off automatic verification**: Before deploying a contract using Hardhat, turn off the automatic contract verification in your `hardhat.config.ts` file by calling

```tsx
tdly.setup({ automaticVerifications: false });
```
{% endhint %}

## Simple manual verification

The simple way to manually verify a contract is to call the `hre.tenderly.verify()` function and provide a reference to the contract you want to verify.

First, deploy the Greeter Smart Contract using Ethers.js. Before the verification code, you have to await for deployment to be confirmed via `await greeter.deployed()`.

```jsx
const Greeter = await ethers.getContractFactory("Greeter");
const greeter = await Greeter.deploy("Hello, Hardhat!");

await greeter.deployed()
```

After deploying the contract, you can verify it using the Tenderly Hardhat plugin.

To successfully verify the contract using the `.verify()` method, you need to pass a configuration object. The object consists of 2 fields:

* the exact **name** of the Smart Contract as it is in the source file, or a fully qualified contract name like "contracts/A/Token.sol:Token".
* the **address** of your deployed Smart Contract&#x20;

If you want to verify multiple contracts, you need to repeat verification for each one.

{% hint style="info" %}
The most common reason why verification fails is a mismatch between the given **`name`** property and the actual name of the Smart Contract.
{% endhint %}

Here’s a script employing this method (`scripts/manual-simple.ts`):

```jsx
// File: scripts/greeter/manual-simple-public.ts
import { ethers, tenderly } from "hardhat";

async function main() {
  const Greeter = await ethers.getContractFactory("Greeter");
  const greeter = await Greeter.deploy("Hello, Manual Hardhat!");

  await greeter.deployed();
  const address = greeter.address;
  console.log("Manual Advanced: {Greeter} deployed to:", address);

  tenderly.verify({
    address,
    name: "Greeter",
  });
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

To perform the verification, run the following:

```bash
npx hardhat run scripts/manual-simple.ts --network ropsten
```

If everything goes well, you should see a similar output in your terminal.

![Output of npx hardhat run scripts/manual-simple.ts --network ropsten](<../../../.gitbook/assets/manual simple terminal>)

## Advanced manual verification

Advanced manual verification allows for the highest level of control over verification parameters. It enables you to specify everything from compiler settings to additional details about each contract you want to verify and the libraries your contracts use.

### Deployment example

Take a look at the code example below that demonstrates the advanced manual verification approach. The Greeter contract uses the `hardhat/console.sol` library, so we need to account for that explicitly.

With more power over configuring the verification process, you need to do provide the following key information for each contract you’re verifying (the `contracts` list):

* **For contracts**: Specify the **source code** of the Greeter Smart Contract and the **address** it’s deployed to on a **specific network** (or several networks).
* **For libraries**: Specify a list of all the libraries referenced by the contract as additional contracts, with the same information you’d provide to specify a contract. If already deployed, you can paste the address to `compiler.settings.libraries` parameter like you would paste in solidity compiler input.

```tsx
// File: scripts/greeter/manual-advanced.ts
import { readFileSync } from "fs";
import { ethers, tenderly } from "hardhat";

export async function main() {
  // deploy stuff but later pretend it's been deployed ages ago on Sepolia.
  const Greeter = await ethers.getContractFactory("Greeter");
  const greeter = await Greeter.deploy("Hello, Manual Hardhat!");

  await greeter.deployed(); // await for the contract to be fully deployed
  
  const greeterAddress = greeter.address;
  console.log("Manual Simple: {Greeter} deployed to", greeterAddress);

  // pretend it's been deployed ages ago on Sepolia in a different deployment.
  // Hence we know NETWORK_ID=11155111 and the address of the contract (greeterAddress)
  const NETWORK_ID = 11155111;
  
  await tenderly.verifyMultiCompilerAPI({
    contracts: [
      {
        contractToVerify: "Greeter",
        sources: {
          "contracts/Greeter.sol": {
            name: "Greeter",
            code: readFileSync("contracts/Greeter.sol", "utf-8").toString(),
          },   
          "hardhat/console.sol": {
            name: "console",
            code: readFileSync(
              "node_modules/hardhat/console.sol",
              "utf-8"
            ).toString(),
          }  
        },
        // solidity format compiler with a little modification at libraries param
        // see the warning below
        compiler: { 
          version: "0.8.17",
          settings: {
            optimizer: {
              enabled: true,
              runs: 200, 
            }
          }
        },
        networks: {
          [NETWORK_ID]: {
            "address": greeterAddress
          }
        }
      },
    ]
  });
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

As seen in the example above, the two core aspects of using the `verifyMultiCompilerApi` are:

* The compiler configuration that was used to compile deployed contracts.
* The list of contracts undergoing verification.

Let’s explore these in detail.

### The Solidity compiler param

`compiler` field is the same type as the official [solidity compiler](https://docs.soliditylang.org/en/v0.8.17/using-the-compiler.html#input-description).

{% hint style="info" %}
Verification can fail if the compiler config you specified differs significantly from the one actually used to compile the Smart Contract deployed on-chain.
{% endhint %}

{% hint style="danger" %}
In order to satisfy our own API, we had to modify the `compiler` object a little bit.\
If you wish to specify libraries for the contracts, add an extra `addresses` param.

```typescript
compiler.settings.libraries = {
    "path/to/lib.sol": {
        addresses: {
            "LibName1": "0x..."
            "LibName2": "0x..."
        }
    }
}
```
{% endhint %}

### The list of _contracts_

The `contracts` property of the configuration is used to specify all the contracts you’re verifying (lines 26-37) and all the Solidity libraries referenced by the contracts (lines 38-49), in a single function call.

Here’s a breakdown of the `contracts` property of the advanced verification configuration:

| Parameter                   | Type   | Description                                                                                                                                                                                                                                                                                                    |
| --------------------------- | ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| contractToVerify            | string | The name of the contract to verify. This can be a short name like `Greeter` or a fully qualified contract name like `contracts/A/Greeter.sol:Greeter`                                                                                                                                                          |
| sources                     | string | A map of all sources that are needed in order to compile the contract. The key of the map is a source path to the contract.                                                                                                                                                                                    |
| sources.key                 | string | <p><strong>For Smart Contracts</strong>, this is a relative path to the Smart Contract, relative to the <code>contracts</code> directory.<br><strong>For libraries</strong>, this is a relative path and it should match the one in the <code>import</code> statement within the Contract that’s using it.</p> |
| sources.key.name            | string | Name of the contract. This must short name format.                                                                                                                                                                                                                                                             |
| networks                    | Object | The set of networks where the contract is deployed. For Libraries that aren’t deployed, pass an empty object `{}`.                                                                                                                                                                                             |
| networks.key                | int    | The ID of a network where contract is deployed (e.g., Mainnet is 1, Rinkeby is 4)                                                                                                                                                                                                                              |
| networks.key.address        | string | The address of a contract deployed on a specific network.                                                                                                                                                                                                                                                      |
| compiler.settings.libraries | Object | Object in which you specify the library dependencies that are needed in order to compile the contract.                                                                                                                                                                                                         |



Take a look at [the Solidity library overview](https://docs.soliditylang.org/en/v0.8.15/contracts.html?highlight=libraries#libraries) for more information.&#x20;

#### Specifying libraries for Tenderly verification

Alongside the Greeter contract, you also need to send an entry corresponding to `hardhat/console.sol` Smart Contract, which is in turn a library. The verification process requires the specification of all the libraries referenced by the Smart Contract.

Here are a few guidelines for specifying libraries:

* **Library source**: Retrieve the contents of `node_modules/hardhat/console.sol` and pass them as the `code` verification parameter.
* **Source path**: Pass `sourcePath`, the path to the library: `hardhat/console.sol`. It’s a relative path and it should match the path in the `import` statement in the Greeter contract.
* **Networks**: Pass an empty object (`{}`) for `networks` because `console.sol` is deployed alongside the Greeter. This means that the contract isn’t deployed separately, so you only have to make it available for the Tenderly Verification process. In the case the library you’re using is deployed on the network, pass the actual address.

When verifying a contract that uses several libraries, each library must be explicitly specified, including the source code. Include the address of the library if it’s pre-deployed on the network or pass an empty network configuration if the library is linked to your contract at compile time.

Explore the [**example project** in the plugin Git repo](https://github.com/Tenderly/hardhat-tenderly/tree/master/examples/contract-verification) to see how to include a **separately deployed contract/library**. The second example (**Calculator** contract) demonstrates this case.
