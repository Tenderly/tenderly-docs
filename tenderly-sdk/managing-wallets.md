---
description: >-
  Use these code snippet examples to add, update, remove, and fetch wallets
  using the Tenderly SDK.
---

# Managing Wallets

The Tenderly SDK provides a **`WalletRepository`** class for managing wallets associated with your project. The **`WalletRepository`** allows you to add, update, and remove wallets.

Once you have initialized the Tenderly SDK, you can use the **`wallets`** namespace to access the **`WalletRepository`** instance.

### **Adding a wallet**

To add a new wallet, use the **`add`** method of the **`wallets`** namespace:

```jsx
try {
  const walletAddress = '0x742d35Cc6634C0532925a3b844Bc454e4438f44e';
	const addedWallet = await tenderly.wallets.add(walletAddress, {
	  displayName: "My Wallet",
	}); 
	console.log("Added wallet:", addedWallet);
} catch(error) {
  console.error("Error adding wallet:", error);
}

```

### **Updating a wallet**

To update an existing wallet, use the **`update`** method of the **`wallets`** namespace:

```jsx
try {  
	const walletAddress = '0x742d35Cc6634C0532925a3b844Bc454e4438f44e';
	const updatedWallet = await tenderly.wallets.update(walletAddress, {
	  displayName: "My Wallet"
	});
	console.log("Updated wallet:", updatedWallet);
} catch(error) {
  console.error("Error updating wallet:", error);
}

```

### Removing **a wallet**

To remove a wallet, use the **`remove`** method of the **`wallets`** namespace:

```jsx
try {
	const walletAddress = '0x742d35Cc6634C0532925a3b844Bc454e4438f44e';
	await tenderly.wallets.remove(walletAddress);
  console.log("Wallet removed successfully");
} catch(error) {
  console.error("Error removing wallet:", error);
}

```

### **Fetching wallets**

To fetch wallets associated with your project, use the **`getAll`** method of the **`wallets`** namespace:

```jsx
try {
	const allWallets = await tenderly.wallets.getAll();
	console.log('All wallets:', allWallets);
} catch(error) {
  console.error("Error fetching wallets:", error);
}

```

### **Fetching a single wallet**

To fetch a single wallet by its ID, use the **`get`** method of the **`wallets`** namespace:

```jsx
try {
	const walletAddress = '0x742d35Cc6634C0532925a3b844Bc454e4438f44e';
	const wallet = await tenderly.wallets.get(walletAddress)
	console.log("Fetched wallet:", wallet);
} catch(error) {
  console.error("Error fetching wallet:", error);
}

```
