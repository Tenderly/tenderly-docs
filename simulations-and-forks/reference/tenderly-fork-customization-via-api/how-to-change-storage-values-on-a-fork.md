---
description: >-
  This call allows you to change any storage slot of any contract, within the
  boundary of the Tenderly Fork you're working with.
---

# How to Change Storage Values on a Fork

If you want to simulate a transaction in a very specific state of the involved contract(s), there are two ways to do it.&#x20;

* You can execute several transactions to get them in the desired state.&#x20;
* Alternatively, you can plant a specific value into one or more storage slots of your Smart Contract(s).&#x20;

If you decide to go with the second option, you need to use `tenderly_setStorageAt` JSON-RPC call.&#x20;

{% hint style="info" %}
This is a custom JSON-RPC call that is applicable only for Tenderly Forks.
{% endhint %}

Here’s an example. You can play around with this using [this Tenderly Sandbox](https://sandbox.tenderly.co/nenad/json-rpc).

```tsx
...
const forkRpcUrl = ...;

const provider = new ethers.providers.JsonRpcProvider(forkRpcUrl);
const two32BHexStr = ethers.utils.hexZeroPad(ethers.utils.hexValue(2), 32);
const fiftyFive32BHexStr = ethers.utils.hexZeroPad(ethers.utils.hexValue(55), 32);

await provider.send("tenderly_setStorageAt", [
  // the contract address
  contractAddress,
  two32BHexStr,
  fiftyFive32BHexStr,
]);

const newValue = await fork.provider.getStorageAt(greeter.address, 2);
```

The first parameter is the contract address, the second is the storage slot, and the third is the value we want to set. The last two parameters have to be a string representation of a 32-byte number.
