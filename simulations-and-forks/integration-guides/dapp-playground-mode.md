---
description: >-
  Learn how to run your dapp in playground mode to showcase its functionalities
  to your end users without spending any gas.
---

# Dapp Playground Mode

## Overview

Learn how to run your dapp in playground mode so you can onboard your users gas-free. Allow your users to explore the functionalities of your dapp without spending any money.&#x20;

To enable playground mode, you need to:

1. Set up requirements and recommendations.
2. Create a Tenderly Fork.
3. Use JSON-RPC as a provider in Ethers.js.
4. Delete the Fork.

## Set up requirements and recommendation

To simplify the integration, we're going to assume that we use `ethers.js` to interact with the blockchain. First, we need to add a way for users to enable/disable playground mode, such as a button or any other UI element.

Let’s see a couple of examples.

### Create a Tenderly Fork

The first step is to create your Tenderly Fork:

```tsx
const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;
const TENDERLY_FORK_API = `http://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/fork`;

const opts = {
    headers: {
        'X-Access-Key': TENDERLY_ACCESS_KEY as string,
    }
}
const body = {
  "network_id": "1",
  "block_number": 14537885,
}

const resp = await axios.post(TENDERLY_FORK_API, body, opts);
```

### Fill the user account with Ether

To really showcase the vast functionality of your dapp, it would probably cost some Ether. No worries, you can always give the user an option to “fill” test ETH from our faucet endpoint.

```tsx
export const fillEther = async (walletAddress: string): Promise<void> => {
    const params = [
            [walletAddress],
            ethers.utils.hexValue(100) // hex encoded wei amount
    ];

    await provider.send('tenderly_addBalance', params)
}
```

### Use JSON-RPC as a provider in Ethers.js

The next step is to use `fork.rpc_endpoint` as `JsonRpcProvider` for the `ethers.js` library.

Spawning Ethers is rather easy:

```tsx
import {ethers} from "ethers"

var tenderlyForkProvider = new ethers.providers.JsonRpcProvider(forkURL);
```

Keep in mind that your dapp has to use `tenderlyForkProvider` when interacting with a smart contract to have it executed within the Fork:

```tsx
const contract = new ethers.Contract(CONTADDRESS , CONTRACT_ABI , provider.getSigner());
```

### Delete the Fork

You can choose when to delete your Tenderly Fork. You can do this either when the user turns off the playground mode or after some predefined TTL expires (e.g. 30mins). You have the flexibility to choose depending on your needs.&#x20;

To delete a Fork, you need to do the following:&#x20;

```tsx
const TENDERLY_FORK_ACCESS_URL = `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/fork/${forkId}`
  const opts = {
      headers: {
          'X-Access-Key': accessKey,
      }
  }

  await axios.delete(TENDERLY_FORK_API, opts);
```

That's it, we're done 🎉

{% hint style="success" %}
Here is the [link to the GitHub repo](https://github.com/Tenderly/integration-samples/tree/main/playround-enviroment-for-dapps) covering this and many other use cases.
{% endhint %}
