# Instant Staging/QA Environment for dApps

## Overview

Every piece of code needs to be tested in one way or the other. For solidity-based smart contracts, it is standard to have at least unit tests, but we all know that an isolated environment is not always ideal for bug prevention. The real-world project is probably going to have a complex frontend integration and even possibly backend services that are helping in the background.

Let’s see how we can spin up an instant staging environment.

## FE-only staging environment

1. Create a Tenderly Fork via UI.
2. Connect ethers with a Tenderly Fork provider.
3. Populate transaction parameters and execute simulation for transactions.

### Create a Tenderly Fork via UI

You can follow our documentation regarding Fork creation, or you can do it yourself 😁

{% content-ref url="../../how-to-create-a-fork/" %}
[how-to-create-a-fork](../../how-to-create-a-fork/)
{% endcontent-ref %}

Once the Fork has been created, you can copy the RPC URL directly from your Dashboard. It should look something like this:&#x20;

`https://rpc.tenderly.co/fork/21981657-3edf-4996-9776-918724c59e78`

### Connect ethers with a Tenderly Fork provider

We recommend that you keep your Fork RPC URL hidden from the public. Here, in this code example, we are going to extract it from the environment variables:

```tsx
const {	TENDERLY_JSON_RPC_URL } = process.env

const provider = new ethers.providers.JsonRpcProvider(TENDERLY_JSON_RPC_URL);
const contract = new ethers.Contract(contractAddress, contractABI, provider)
```

### Populate transaction parameters and execute simulation for transactions

Now that we have our provider and our contract instance, let’s run a transaction simulation in Tenderly Fork signed by the user's wallet address. Keep in mind that every account is automatically unlocked when performing simulations.&#x20;

This enables you to impersonate any address and send transactions, even as smart contracts:

```tsx
const unsignedTx = await contract.populateTransaction[funcName](...args)
const transactionParameters = [{
    to: contract.address,
    from: sender,
    data: unsignedTx.data,
    gas: ethers.utils.hexValue(300000),
    gasPrice: ethers.utils.hexValue(1),
    value: ethers.utils.hexValue(0)
}];

const txHash = await provider.send('eth_sendTransaction', transactionParameters)
```

That’s it, you are all set 🎉

Make sure to propagate the `provider` in every `ethers.js` contract instance and use it in all interactions.

## BE + FE staging environment

Alternatively, you can have your backend service create a Fork and propagate the RPC URL of the Tenderly fork to your frontend.

Here are the steps:

1. Generate an API access key.
2. Create Tenderly Fork by a backend service.
3. Report RPC URL of Tenderly Fork to the FE.
4. Connect ethers.js in FE.

### Obtain Tenderly API access key

The access key is needed in order to interact with Tenderly API. If you don’t have it already, here’s how you can get it:

{% content-ref url="../configuration-of-api-access.md" %}
[configuration-of-api-access.md](../configuration-of-api-access.md)
{% endcontent-ref %}

### Obtain Tenderly Fork via backend service

Rather than via UI, we are going to create our Tenderly Fork environment via API.

Let’s do it for Ethereum **Mainnet** on the **14386016** block number.

```tsx
const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;
const TENDERLY_FORK_API = `http://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/fork`;

const opts = {
    headers: {,
        'X-Access-Key': TENDERLY_ACCESS_KEY,
  }
}

const body = {
    "network_id": "1",
    "block_number": "14386016",
}

const resp = await axios.post(TENDERLY_FORK_API, body, opts);

const forkId = resp.data.simulation_fork.id
const forkRPC = `https://rpc.tenderly.co/fork/${forkId}`
```

### Forward RPC URL of Tenderly Fork to the FE

Now that we have created the Fork environment on the backend service, let’s forward the Fork URL to the FE but feel free to consume it in the BE also.

How you should tackle this step is up to you. Here are some ideas:

* Expose an HTTP route for creating a Fork environment. FE can invoke it and then consume RPC endpoint directly.
* Have a proxy service that would route every JSON RPC request from FE through your backend service to the Tenderly JSON-RPC.

### Connect ethers.js in the dApp

Let’s remind ourselves just how easy it is to set up ethers.js

```tsx
const provider = new ethers.providers.JsonRpcProvider(forkRPC);
```

Woohoo, everything is done 🎉

{% hint style="success" %}
You can visit our GitHub repo and find the the dummy implementation of the above example [on the following link](https://github.com/Tenderly/integration-samples/tree/main/staging-enviroment-for-dapps).
{% endhint %}
