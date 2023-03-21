---
description: Learn how to change a network ID by specifying a particular chain_id.
---

# How to Specify/Change Network chain\_id

We generally use `chain_id` as part of transaction signing. In most cases, it's the same as the originating network. But what if you'd like to change it?&#x20;

For instance, you can change the network ID to prevent a Fork environment from producing a signature valid on the actual network, stopping a transaction from replaying an attack:

```tsx
...

const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;
const TENDERLY_FORK_API = `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/fork`

const body = {
  "network_id": "1", // network you wish to fork
  "block_number": 14386016,
  "chain_config": {
    "chain_id": 3 // chain_id used in the forked environment
  }
}

const resp = await axios.post(TENDERLY_FORK_API, body, opts);
```
