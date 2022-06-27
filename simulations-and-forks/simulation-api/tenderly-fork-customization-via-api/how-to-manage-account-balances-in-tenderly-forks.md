# How to manage Account Balances in Tenderly Forks

If you’re using forks, you may need to manage the value of accounts’ balances. Tenderly’s custom JSON RPC enables changing the balances of accounts in Tenderly Forks: you can set a specific value or increase the value by an amount.

This snippet sets the balance of address `0x0d2026b3EE6eC71FC6746ADb6311F6d3Ba1C000B` to value of `0xDE0B6B3A7640000` Wei, using the `tenderly_addBalance` custom RPC endpoint.

```jsx
provider.send("tenderly_setBalance", {
    "jsonrpc": "2.0",
    "method": "tenderly_setBalance",
    "params": [
	["0x0d2026b3EE6eC71FC6746ADb6311F6d3Ba1C000B"], // address(es)
        "0xDE0B6B3A7640000", // amount in Wei
     ],
    "id": "1234"
});
```

Alternatively, you can top-up the balance of specified addresses by an amount, using `tenderly_addBalance` custom RPC endpoint

```jsx
provider.send("tenderly_addBalance", {
    "jsonrpc": "2.0",
    "method": "tenderly_addBalance",
    "params": [
	["0x0d2026b3EE6eC71FC6746ADb6311F6d3Ba1C000B"], // address(es)
	"0xDE0B6B3A7640000", // amount in Wei
     ],
    "id": "1234"
});
```
