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

To verify a contract's source code, use the **`verify`** method of the **`contracts`** namespace:

```javascript
const verificationReq = {
	config: {
    mode: 'public', // 'private' is also possible
	},
  contractToVerify: 'Counter.sol:Counter',
  solc: {
    version: 'v0.8.18',
    sources: {
      'Counter.sol': {
        content: counterContractSource,
      },
    },
    settings: {
      libraries: {},
      optimizer: {
        enabled: false,
      },
    },
  },
}

tenderly.contracts.verify(address, verificationRequest).then((verificationResult) => {
  console.log("Verification result:", verificationResult);
}).catch((error) => {
  console.error("Error verifying contract:", error);
});
```
