---
description: >-
  Learn how to create an instant dapp staging environment for frontend and
  backend purposes.
---

# Instant Staging/QA Environment for Dapps

## Overview&#x20;

Welcome to the detailed guide on creating an instant staging environment for your dapp. We will lead you through the process of creating a staging environment that uses real-time blockchain data in this guide. You will be able to conduct numerous tests on your smart contract code by following these procedures, ensuring its stability and dependability.&#x20;

When creating a dapp, it is critical to properly test both the frontend integration and the backend services. While an isolated environment is beneficial for bug prevention, it may not accurately represent the complexities of a real-world project. By employing real-time blockchain data, an instant staging environment delivers a more realistic testing environment.

Now, let's dive into the step-by-step process of creating an instant staging environment for your dapp:

## FE-only staging environment

To create a staging environment for frontend testing, you need to complete the following steps:&#x20;

1. Create a Tenderly Fork via the UI.
2. Connect ethers with a Tenderly Fork provider.
3. Populate transaction parameters and execute a transaction simulation.

### Step 1: Create a Tenderly Fork via the UI

To create a Tenderly Fork from the Dashboard, you can follow this guide:&#x20;

{% content-ref url="../forks/using-forks-ui.md" %}
[using-forks-ui.md](../forks/using-forks-ui.md)
{% endcontent-ref %}

Once the Fork has been created, you can copy the RPC URL directly from your Dashboard. It should look something like this:&#x20;

`https://rpc.tenderly.co/fork/21981657-3edf-4996-9776-918724c59e78`

### Step 2: Connect ethers with a Tenderly Fork provider

We recommend that you keep your Fork RPC URL hidden from the public. Here, in this code example, we'll extract it from the environment variables:

```tsx
const {	TENDERLY_JSON_RPC_URL } = process.env

const provider = new ethers.providers.JsonRpcProvider(TENDERLY_JSON_RPC_URL);
const contract = new ethers.Contract(contractAddress, contractABI, provider)
```

### Step 3: Populate transaction parameters and execute a transaction simulation

Now that we have our provider and our contract instance, let’s run a transaction simulation on a Tenderly Fork signed by the user's wallet address. Keep in mind that every account is automatically unlocked when performing simulations.&#x20;

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

That’s it, you're all set 🎉

Make sure to propagate the `provider` in every `ethers.js` contract instance and use it in all interactions.

## BE + FE staging environment

Alternatively, you can have your backend service create a Fork and propagate the RPC URL of the Tenderly Fork to your frontend.

Here are the needed steps:

1. Generate an API access key.
2. Create a Tenderly Fork via a backend service.
3. Report RPC URL of Tenderly Fork to the FE.
4. Connect ethers.js in FE.

### Step 1: Obtain the Tenderly API access key

You need the access key to interact with Tenderly API. If you don’t have it already, here’s how you can get it:

{% content-ref url="../reference/configuration-of-api-access.md" %}
[configuration-of-api-access.md](../reference/configuration-of-api-access.md)
{% endcontent-ref %}

#### Step 2: Create a Tenderly Fork via a backend service

We're going to create our Tenderly Fork environment via API rather than the Tenderly UI.

Let’s do it for the Ethereum **Mainnet** on the **14386016** block number.

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
    "block_number": 14386016,
}

const resp = await axios.post(TENDERLY_FORK_API, body, opts);

const forkId = resp.data.simulation_fork.id
const forkRPC = `https://rpc.tenderly.co/fork/${forkId}`
```

### Step 3: Forward the Fork RPC URL to the FE

After creating a Fork via a backend service, let’s forward the Fork URL to the FE but feel free to use it in the BE as well.

Here are some ideas that can help you get started:&#x20;

* Expose an HTTP route for creating a Fork environment. The FE can invoke it and then consume the RPC endpoint directly.
* Have a proxy service that would route every JSON-RPC request from FE through your backend service to the Tenderly JSON-RPC.

### Step 4: Connect ethers.js in the dApp

Let’s remind ourselves just how easy it is to set up ethers.js

```tsx
const provider = new ethers.providers.JsonRpcProvider(forkRPC);
```

## Recap

What did we just do? Well, you just created a staging evironment for your dapp based on real-time blockchain data with Tenderly 🎉

By following the steps demonstrated in this comprehensive guide, you have unlocked a valuable tool that will considerably improve your dapp development process. Remember that your staging environment is more than just a testing ground. It is an essential part of your dapp development workflow, allowing you to confidently iterate, debug, and refine your code. Tenderly gives you access to a complete set of features and tools that will help you optimize your testing process and develop a high-quality dapp that fulfills the needs of your users.

{% hint style="success" %}
You can visit our GitHub repo for a [dummy implementation of the above example](https://github.com/Tenderly/integration-samples/tree/main/staging-enviroment-for-dapps).
{% endhint %}
