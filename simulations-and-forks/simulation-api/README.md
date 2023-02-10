---
description: >-
  Learn how to use Simulation API to understand transaction execution before
  deployment, provide more visibility into a transaction's effects, avoid
  undesirable outcomes, and build confidence.
---

# Simulation API

## Overview

Simulation API allows you to understand a transaction's execution against any point in a network's history, including the latest block, but without sending it to the blockchain. The API gives you access to a lightweight blockchain execution environment that delivers detailed information about state changes, emitted events (logs), gas usage, and all calls that the transaction made. Since simulations don't run on an actual network, it's a gas-free way to test "what-if" scenarios.

You can use this information for various smart contract development purposes or to influence decision making in your dapp code. You can even provide it to end users and empower them to confidently use your dapp.

Here are some examples of what you can achieve with Simulation API:

* Dry-run user transactions to help them save money on failed txs and improve your dapp UX
* [Run your dapp in playground mode](integration-guides/dapp-playground-mode.md) to let users try out your dapp without spending any gas and with all production data readily available
* [Stage QA environments](integration-guides/instant-staging-qa-environment-for-dapps.md) for a blockchain project
* [Set up CI/CD](integration-guides/ci-cd-pipeline-for-smart-contracts.md) for your blockchain project
* Validate complex DAO governance proposals

## How to start using Tenderly Simulation API

Follow the next steps in order to start using simulations:

1. [Create a one-off simulation](./#1-create-a-one-off-simulation)
2. [Consume the decoded simulation result](advanced-simulation-api.md)
3. [Override smart contracts' state](simulation-api-with-state-overrides.md) when simulating
4. [Perform a bundled simulation](bundled-simulations.md) - simulating multiple transactions at once
5. [Create Fork environment](./#2-create-a-fork-environment)
6. [Add Ether to your test address](./#3-add-ether-to-your-test-address)
7. [Execute transaction in Tenderly Fork](./#4-execute-transaction-in-tenderly-fork)
8. [Delete the fork](./#5-delete-the-fork)

### 0 Set up the API

To get your Access Token, go to the [**Settings > Authorization**](https://dashboard.tenderly.co/account/authorization) and click on **Create Access Token**. If you want to create an organization token you can do so from your [organization’s settings page](https://dashboard.tenderly.co/organizations).

The token you get will be used in API authentication.

{% hint style="warning" %}
Do not share the API Access token freely.
{% endhint %}

You should have these variables exposed to your code, as shown in this `.env` file:

```bash
TENDERLY_ACCESS_KEY=... # obtain it from the dashboard
TENDERLY_PROJECT=... # project slug
TENDERLY_USER=... # your username
```

You can find more details here:

{% content-ref url="configuration-of-api-access.md" %}
[configuration-of-api-access.md](configuration-of-api-access.md)
{% endcontent-ref %}

### 1 Create a one-off simulation

We can start by simulating a transaction. We'll see its execution without recording any state changes. You can get the output of the transaction, see whether it failed or not, what it changed, the contracts it called, and more. All of this information is available without actually sending the transaction to the chain, with no gas fees. You can simulate any transaction using any given contract deployed on networks available in Tenderly.

Let's simulate the Uniswap `swapTokensForExactTokens` function and access state changes, logs, and call traces to extract relevant data.&#x20;

{% hint style="info" %}
#### Quick vs Full simulations

Simulation API comes in two modes you can specify to the `simulation_type` parameter.

* The default **full** mode gives you decoded simulation results, matched to the smart contracts code, for easier client-side interpretation
* The **quick** mode provides you raw transaction results, in less time.



#### Saving Simulations

* To persist simulations so they're visible in Tenderly dashboard, use the boolean `save` parameter.
* To persist only failing simulations, use `save_if_fails` boolean flag.&#x20;
{% endhint %}

**Example (typescript)**

Lines 11-41 represent the invocation of the API. The rest shows some information you can extract from this simulation.

Notice we're doing a `quick` simulation, and we've set `save` to `true`, so simulation will appear in Simulations page in the Dashboard.

{% code lineNumbers="true" %}
```typescript
import axios from 'axios';
import * as dotenv from 'dotenv';
dotenv.config();

const approveDai = async () => {
  // assuming environment variables TENDERLY_USER, TENDERLY_PROJECT and TENDERLY_ACCESS_KEY are set
  // https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name
  // https://docs.tenderly.co/other/platform-access/how-to-generate-api-access-tokens
  const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;

  console.time('Simulation');

  const resp = await axios.post(
    `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/simulate`,
    // the transaction
    {
      /* Simulation Configuration */
      save: true, // if true simulation is saved and shows up in the dashboard
      save_if_fails: false, // if true, reverting simulations show up in the dashboard
      simulation_type: 'quick', // full or quick (full is default)

      network_id: '1', // network to simulate on

      /* Standard EVM Transaction object */
      from: '0xdc6bdc37b2714ee601734cf55a05625c9e512461',
      to: '0x6b175474e89094c44da98b954eedeac495271d0f',
      input:
        '0x095ea7b3000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1000000000000000000000000000000000000000000000000000000000000012b',
      gas: 8000000,
      gas_price: 0,
      value: 0,
    },
    {
      headers: {
        'X-Access-Key': TENDERLY_ACCESS_KEY as string,
      },
    }
  );
  console.timeEnd('Simulation');

  const transcation = resp.data.transaction;

  console.log(
    `Simulated transaction info: 
  hash: ${transcation.hash} 
  block number: ${transcation.block_number}
  gas used: ${transcation.gas_used}`,
  '\n\n'
  );

  console.log('Events');
  console.log(
    JSON.stringify(resp.data.transaction.transaction_info.logs, null, 2),
    '\n\n'
  );

  console.log('State changes');
  console.log(
    JSON.stringify(
      resp.data.transaction.transaction_info.call_trace.state_diff,
      null,
      2
    ),
    '\n\n'
  );
  console.log('Call Trace');
  console.log(
    JSON.stringify(resp.data.transaction.transaction_info.call_trace, null, 2)
  );
};

approveDai();
```
{% endcode %}

The output shows something similar to this:

```
Simulation: 261.775ms
Simulated transaction info: 
  hash: 0x1e44c2d964c9805b235475e55c31c27785aa2fc00129d2a4b21ed5eed6928929 
  block number: 16548464
  gas used: 46098 


Events
[
  {
    "name": "",
    "anonymous": false,
    "inputs": null,
    "raw": {
      "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
      "topics": [
        "0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925",
        "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
        "0x000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
      ],
      "data": "0x000000000000000000000000000000000000000000000000000000000000012b"
    }
  }
] 


State changes
[
  {
    "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
    "soltype": null,
    "original": null,
    "dirty": null,
    "raw": [
      {
        "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "key": "0xe11925e259d23a0e30bc90c0742b3349668b7689af7f13b99127b4837cd9c78f",
        "original": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "dirty": "0x000000000000000000000000000000000000000000000000000000000000012b"
      }
    ]
  }
] 


Call Trace
{
  "hash": "0x1e44c2d964c9805b235475e55c31c27785aa2fc00129d2a4b21ed5eed6928929",
  "contract_name": "",
  "function_pc": 0,
  "function_op": "CALL",
  "absolute_position": 0,
  "caller_pc": 0,
  "caller_op": "CALL",
  "call_type": "CALL",
  "from": "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
  "from_balance": "0",
  "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
  "to_balance": "0",
  "value": "0",
  "block_timestamp": "0001-01-01T00:00:00Z",
  "gas": 7978416,
  "gas_used": 24514,
  "intrinsic_gas": 21584,
  "input": "0x095ea7b3000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1000000000000000000000000000000000000000000000000000000000000012b",
  "nonce_diff": [
    {
      "address": "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
      "original": "0",
      "dirty": "1"
    }
  ],
  "state_diff": [
    {
      "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
      "soltype": null,
      "original": null,
      "dirty": null,
      "raw": [
        {
          "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
          "key": "0xe11925e259d23a0e30bc90c0742b3349668b7689af7f13b99127b4837cd9c78f",
          "original": "0x0000000000000000000000000000000000000000000000000000000000000000",
          "dirty": "0x000000000000000000000000000000000000000000000000000000000000012b"
        }
      ]
    }
  ],
  "logs": [
    {
      "name": "",
      "anonymous": false,
      "inputs": null,
      "raw": {
        "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "topics": [
          "0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925",
          "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
          "0x000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
        ],
        "data": "0x000000000000000000000000000000000000000000000000000000000000012b"
      }
    }
  ],
  "output": "0x0000000000000000000000000000000000000000000000000000000000000001",
  "decoded_output": null,
  "network_id": "1",
  "calls": null
}
```

### 2 Create a Fork environment

Next, after we have executed a one-off simulation let’s execute them together. We are going to execute them under the “forked” environment. You can imagine it as if time has stopped on a specific block and only we can execute simulated transactions that would apply to the desired chain.

Here we are going to fork the Ethereum **Mainnet** on block **14386016**:

**API Typescript**

```tsx
import * as dotenv from "dotenv"
import axios from 'axios';

dotenv.config(); // load environment variables using dotenv 
const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;

const TENDERLY_FORK_API = `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/fork`

// set up your access-key, if you don't have one or you want to generate new one follow next link
// https://dashboard.tenderly.co/account/authorization
const opts = {
      headers: {
          'X-Access-Key': TENDERLY_ACCESS_KEY as string,
    }
  }

const body = {
  "network_id": "1",
  "block_number": 14386016,
}

axios.post(TENDERLY_FORK_API, body, opts)
    .then(res => {
        console.log(`Forked with fork ID ${res.data.simulation_fork.id}. Check the Dashboard!`);
    }).catch(err => console.error(err))
```

#### 2.1 Using Fork with ethers.js

After creating a Tenderly Fork, you can interact with its JSON-RPC API, returned through `simulation_fork.rpc_url`. After, you can spawn ethers.js with any other network you are using or plan to use.

{% hint style="success" %}
**Tenderly will create 10 test addresses with 100 ETH each**. By default, ethers.js will do transaction signing with the 0th address as the default signer.
{% endhint %}

**API Typescript**

```tsx
import {ethers} from "ethers";

...

const forkId = resp.data.simulation_fork.id
const forkRPC = `https://rpc.tenderly.co/fork/${forkId}`

const provider = new ethers.providers.JsonRpcProvider(forkRPC);
const signer = provider.getSigner()
```

### 3 Add Ether to your test address

As one of the first actions on top of the Forked environment let’s add Ether to your wallet address that would be used to send transactions. There are a couple of options for how we can do this, we can just simulate transactions and transfer Ethers from one address to our own (every address is automatically unlocked) or we can just mint new Ether.

Let’s see how we can mint new Ether to our test address. Here we’re using the custom Tenderly JSON-RPC endpoint `tenderly_addBalance`.

**API Typescript**

```tsx
const params = [
        [YOUR_WALLET_ADDRESS],
        ethers.utils.hexValue(100) // hex encoded wei amount
];

await provider.send('tenderly_addBalance', params)
```

### 4 Execute transaction in Tenderly Fork

Now that we have enough Ethers to cover all gas costs for our transactions. Let’s start to chain transaction simulations, we are going to execute `approve()` and `transferFrom()` functions on top of the DAI contract.

{% hint style="info" %}
When specifying BigNumberish fields for transaction payload in a form of a hexadecimal string, these **must not contain leading zeros**. \
Use [`ethers.utils.hexValue(aBigNumberish)`](https://docs.ethers.io/v5/api/utils/bytes/#utils-hexValue) to convert the given bigNumberish value into acceptable form with no leading zeros.
{% endhint %}

We can use the provider we have created in 2.1 with ethers.js.

**API Typescript**

```tsx
const DAI_ADDRESS = "0x6B175474E89094C44Da98b954EedeAC495271d0F";
const DAI_ABI = "{...}";

const daiContract = new ethers.Contract(DAI_ADDRESS , DAI_ABI , signer);

// converts 1 ether into wei, stripping the leading zeros
const tokenAmount = ethers.utils.hexValue(utils.parseEther('1').toHexString(10));

// Keep in mind that every account is automatically unlocked when performing simulations.
// This enables you to impersonate any address and send transactions. 
const unsignedTx = await contract.populateTransaction.approve(await signer.GetAddress(), tokenAmount)
const transactionParameters = [{
    to: contract.address,
    from: ZERO_ADDRESS,
    data: unsignedTx.data,
    gas: ethers.utils.hexValue(3000000),
    gasPrice: ethers.utils.hexValue(1),
    value: ethers.utils.hexValue(0)
}];
const txHash = await provider.send('eth_sendTransaction', transactionParameters)

const respTxTransfer = await daiContract.transferFrom(ZERO_ADDRESS, YOUR_ADDRESS, tokenAmount);
```

### 5 Delete the fork

At the end of your execution, we should delete the Fork. This would remove any unnecessary clutter from the UI and also our infrastructure would be grateful 🙏

**API Typescript**

```tsx
const TENDERLY_FORK_ACCESS_URL = `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/fork/${forkId}`

await axios.delete(TENDERLY_FORK_ACCESS_URL, opts)
```

{% hint style="success" %}
In the following articles you will find specific code examples in some places. If you want to browse our code repo immediately you can find it in [**this GitHub repo**](https://github.com/Tenderly/integration-samples).
{% endhint %}

{% hint style="info" %}
You can check out the [plans and pricing for the Simulation API here](simulation-api-rate-limits.md). You can also check out all [Public API endpoints here](https://docs-api.tenderly.co/) - this documentation space is under continuous development, so if you need some API endpoints that aren't available or other API needs that aren't listed publicly, please ping us via [**Intercom on the Tenderly Dashboard**](https://dashboard.tenderly.co/) **** and we'll do our best to meet your needs 🖖
{% endhint %}
