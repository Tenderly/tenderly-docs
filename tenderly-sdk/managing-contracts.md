---
description: >-
  Use these code snippet examples to add, update, remove, and verify smart
  contracts using the Tenderly SDK.
---

# Managing Contracts

The Tenderly SDK provides a `ContractRepository` class for managing contracts associated with your Tenderly project. The `ContractRepository` allows you to add, update, and remove contracts, as well as verify them.

With the Tenderly SDK initialized, you can use the **`contracts`** namespace to access the **`ContractRepository`** instance.

### **Adding a contract**

To add a new contract, use the `add` method of the **`contracts`** namespace:

```jsx
try {
	const contractAddress = '0x742d35Cc6634C0532925a3b844Bc454e4438f44e';
	const contract = await tenderly.contracts.add(contractAddress, {
		displayName: "MyContract"
	});
	
	console.log("Added contract:", addedContract);
	
} catch(error) {
  console.error("Error adding contract:", error);
}

```

### **Updating a contract**

To update an existing contract, use the **`update`** method of the **`contracts`** namespace:

```jsx
try {  
	const contractAddress = '0x742d35Cc6634C0532925a3b844Bc454e4438f44e';
	const contract = await tenderly.contracts.update(contractAddress, {
	  displayName: "My Contract"
	});
	console.log("Updated contract:", contract);
} catch(error) {
  console.error("Error updating contract:", error);
}

```

### Removing **a contract**

To remove a contract, use the `remove` method of the **`contracts`** namespace:

```jsx
try {
	const contractAddress = '0x742d35Cc6634C0532925a3b844Bc454e4438f44e';
	await tenderly.contracts.remove(contractAddress);
  console.log("Contract removed successfully");
} catch(error) {
  console.error("Error removing contract:", error);
}

```

### **Verifying a contract**

To verify a contract, you can use **`verify`** method of the **`contracts`** namespace.

There are three examples that show the usage of `tenderly.contracts.verify` method:

* First example shows the verification of a simple `Counter` contract with no dependencies.
* Second example shows the verification of a `MyToken` contract that has multiple dependencies which are other contracts.
* Third example shows the verification of a `LibraryToken` contract that has a library dependency.

You can find these examples in the [examples folder](https://github.com/Tenderly/tenderly-sdk/tree/master/examples/contractVerification) of our `tenderly-sdk` repo along with the instructions on how to start them. Here will be shown only a `MyToken` contract with a few dependencies so you can see how to import them:

```javascript
const myTokenAddress = `0x1a273A64C89CC45aBa798B1bC31B416A199Be3b3`.toLowerCase() as Web3Address;
const ROOT_FOLDER = `examples/contractVerification/withDependencies/contracts`;

const tenderly = new Tenderly({
  accessKey: process.env.TENDERLY_ACCESS_KEY || ``,
  accountName: process.env.TENDERLY_ACCOUNT_NAME || ``,
  projectName: process.env.TENDERLY_PROJECT_NAME || ``,
  network: Network.SEPOLIA,
});

const result = await tenderly.contracts.verify(myTokenAddress, {
  config: {
    mode: `public`,
  },
  contractToVerify: `${ROOT_FOLDER}/MyToken.sol:MyToken`,
  solc: {
    version: `v0.8.19`,
    sources: {
      [`${ROOT_FOLDER}/MyToken.sol`]: {
        content: readFileSync(`${ROOT_FOLDER}/MyToken.sol`, `utf8`),
      },
      [`@openzeppelin/contracts/token/ERC20/ERC20.sol`]: {
        content: readFileSync(`${ROOT_FOLDER}/ERC20.sol`, `utf8`),
      },
      [`@openzeppelin/contracts/token/ERC20/IERC20.sol`]: {
        content: readFileSync(`${ROOT_FOLDER}/IERC20.sol`, `utf8`),
      },
      [`@openzeppelin/contracts/token/ERC20/extensions/IERC20Metadata.sol`]: {
        content: readFileSync(`${ROOT_FOLDER}/IERC20Metadata.sol`, `utf8`),
      },
      [`@openzeppelin/contracts/utils/Context.sol`]: {
        content: readFileSync(`${ROOT_FOLDER}/Context.sol`, `utf8`),
      },
    },
    settings: {
      optimizer: {
        enabled: true,
        runs: 200,
      },
    },
  },
});

console.log(`Result:`, result);

```
