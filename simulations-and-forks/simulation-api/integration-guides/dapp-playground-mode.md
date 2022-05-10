# DApp playground mode

## Overview

Onboarding users to the dApp application is really hard. You cannot showcase the functionality without actually spending user money. But what if you could?&#x20;

We are going to take a look at how you can spin up a **playground** mode of your dApp where users interact with it without actually spending any real funds.

Let’s see what needs to be done in order to enable playground mode:

1. Setup requirements and recommendations.
2. Create a Tenderly Fork.
3. Use JSON RPC as a provider in Ethers.js.
4. Delete the Fork.

## Setup requirements and recommendation

In order to simplify the integration, we are going to assume that we use `ethers.js` for interactions with the blockchain. The first step is to add some way for users to enable/disable playground mode - you can imagine it as a button or any other UI element.

Let’s see a couple of examples of how this can look.

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

### Fill user account with Ether

To really showcase the vast functionality of your dApp it would probably cost a bit of Ether. No worries, as you can always give the User an option to “Fill” ethers from our faucet endpoint.

```tsx
export const fillEther = async (walletAddress: string): Promise<void> => {
    const params = [
            [walletAddress],
            ethers.utils.hexValue(100) // hex encoded wei amount
    ];

    await provider.send('tenderly_addBalance', params)
}
```

### Use JSON RPC as a provider in Ethers.js

The next step is to use `fork.rpc_endpoint` as `JsonRpcProvider` for the `ethers.js` library.

Spawning Ethers is rather easy:

```tsx
import {ethers} from "ethers"

var tenderlyForkProvider = new ethers.providers.JsonRpcProvider(forkURL);
```

Keep in mind that your app has to use `tenderlyForkProvider` when interacting with the smart contract in order to have them executed within the fork:

```tsx
const contract = new ethers.Contract(CONTADDRESS , CONTRACT_ABI , provider.getSigner());
```

### Delete the Fork

You can choose when you would like to Delete your Tenderly Fork - either when the user turns off the playground mode or after some predefined TTL expires (e.g. 30mins), this part is up to you. But, let’s see how this is done:

```tsx
const TENDERLY_FORK_ACCESS_URL = `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/fork/${forkId}`
  const opts = {
      headers: {
          'X-Access-Key': accessKey,
      }
  }

  await axios.delete(TENDERLY_FORK_API, opts);
```

That's it, we are done 🎉

{% hint style="success" %}
Here is the [link](https://github.com/Tenderly/integration-samples/tree/main/playround-enviroment-for-dapps) to the GitHub repo covering this and many other use-cases.
{% endhint %}
