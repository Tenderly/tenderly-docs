# How to Manage Account Balances in Tenderly Forks

If you’re using Tenderly Forks, you may need to manage the value of accounts’ balances. Tenderly’s custom JSON RPC enables you to change the balances of accounts in Tenderly Forks. In other words, you can set a specific value or increase the value by desired amount.

This snippet sets the balance of address `0x0d2026b3EE6eC71FC6746ADb6311F6d3Ba1C000B` to value of `0xDE0B6B3A7640000` Wei, using the `tenderly_addBalance` custom RPC endpoint.

```jsx
provider.send("tenderly_setBalance", {
    "jsonrpc": "2.0",
    "method": "tenderly_setBalance",
    "params": [
	["0x0d2026b3EE6eC71FC6746ADb6311F6d3Ba1C000B"], // address(es)
        "0xDE0B6B3A7640000", // amount in Wei
     ],
     "id": "1"  // optional pass-through parameter
});
```

Alternatively, you can topup the balance of specified addresses by an desired amount, by using `tenderly_addBalance` custom RPC endpoint.

```jsx
provider.send("tenderly_addBalance", {
    "jsonrpc": "2.0",
    "method": "tenderly_addBalance",
    "params": [
	["0x0d2026b3EE6eC71FC6746ADb6311F6d3Ba1C000B"], // address(es)
	"0xDE0B6B3A7640000", // amount in Wei
     ],
    "id": "1" // optional pass-through parameter
});
```
