---
description: Find out how to increase a block number by an arbitrary value.
---

# How to Advance/Mine the Block

In general, every simulation on top of a Tenderly Fork increases the block number. Here's a quick example showing you how to increase it by an arbitrary value.

We're going to use a custom Tenderly RPC call – `evm_increaseBlocks:`

```tsx
...

const params = [
  ethers.utils.hexValue(10) // hex encoded number of blocks to increase
];

await provider.send('evm_increaseBlocks', params)
```
