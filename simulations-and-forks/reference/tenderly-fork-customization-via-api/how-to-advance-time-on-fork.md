---
description: Learn how to advance time on a Fork to validate your hypotheses.
---

# How to Advance Time on Fork

Let’s say you have spawned a Tenderly Fork and now you have a hypothesis around X which may be time-dependent. To validate it, you can increase the current time of the network you forked.&#x20;

For example, you can see if a DAO proposal is going to be impacted by expiration or if there's a time lock implemented in the smart contract itself.

Let’s see how we can achieve this:

```tsx
...

const params = [
  ethers.utils.hexValue(24 * 60 * 60) // hex encoded number of seconds
];

await provider.send('evm_increaseTime', params)
```
