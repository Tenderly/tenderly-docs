# How to advance/mine the block

In general, every Simulation on top of the Tenderly Fork would increase the block number. Here we are going to show you how to increase it by an arbitrary value.

We are going to utilize a custom tenderly RPC call `evm_increaseBlocks:`

```tsx
...

const params = [
        ethers.utils.hexValue(10) // hex encoded number of blocks to increase
];

await provider.send('evm_increaseBlocks', params)
```
