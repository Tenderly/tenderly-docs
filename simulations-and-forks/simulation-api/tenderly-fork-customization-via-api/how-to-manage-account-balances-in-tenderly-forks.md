# How to Manage Account Balances in Tenderly Forks

If you’re using Tenderly Forks, you may need to manage the balance value of a specific account. Tenderly’s custom JSON RPC allows you to change the balances of accounts in Tenderly Forks. In other words, you can set a specific value or increase it by a desired amount.

## Set a Specific Balance

The code snippet below sets the balance value to 100 ETH for one or more addresses using the `tenderly_setBalance` custom RPC endpoint. This endpoint receives two arguments: an array of wallets and the new amount you wish to set in Wei.

```jsx
const WALLETS = [
  "0x....",
  "0x....",
];

const result = await provider.send("tenderly_setBalance", [
  WALLETS,
  //amount in wei will be set for all wallets
  ethers.utils.hexValue(ethers.utils.parseUnits("10", "ether").toHexString()),
]);

```

## Increase the Balance by a Specific Value

To increase the balance of specified addresses by a desired amount, use the `tenderly_addBalance` custom RPC endpoint.&#x20;

```jsx
const WALLETS = [
  "0x....",
  "0x....",
];

const result = await provider.send("tenderly_addBalance", [
  WALLETS,
  //amount in wei will be added for all wallets
  ethers.utils.hexValue(ethers.utils.parseUnits("10", "ether").toHexString()),
]);

```

## Get the Current Balance

To check the balance of an address, use the JSON-RPC endpoint `eth_getBalance`. This endpoint receives two arguments: the address and the block number (or `latest`).

```typescript
const newBalances = await Promise.all(
  WALLETS.map(async (wallet) => ({
    wallet,
    balance: await provider.send("eth_getBalance", [wallet, "latest"]),
  }))
);

console.log("New balances", newBalances);
```
