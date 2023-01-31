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
* Run your dapp in playground mode to let users try out your dapp without spending any gas and with all production data readily available
* Stage QA environments for a blockchain project
* Set up CI/CD for your blockchain project
* Validate complex DAO governance proposals

## How to start using Tenderly Simulation API

Follow the next steps in order to start using simulations:

1. Create a one-off simulation
2. Create Fork environment
3. Add Ether to your test address
4. Execute transaction in Tenderly Fork
5. Delete the fork

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

We can start by simulating a transaction. We'll see its execution without recording any state changes. You can get the output of the transaction, see whether it failed or not, what it changed, the contracts it called, and more. All of this information is available without actually sending the transaction to the chain. You can simulate any transaction using any given contract deployed on networks available in Tenderly.

Let's simulate the Uniswap `swapTokensForExactTokens` function and access state changes, logs, and call traces to extract relevant data.&#x20;

**Example (typescript)**

Lines 11-41 represent the invocation of the API. The rest shows some information you can extract from this simulation.

{% code lineNumbers="true" %}
````typescript
import axios from 'axios';
import * as dotenv from 'dotenv';
dotenv.config();

const simulateUniswap = async () => {
  // assuming environment variables TENDERLY_USER, TENDERLY_PROJECT and TENDERLY_ACCESS_KEY are set
  // https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name
  // https://docs.tenderly.co/other/platform-access/how-to-generate-api-access-tokens
  const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;

  const resp = await axios.post( `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/simulate`,
    // the transaction
    {
      // Simulation configuration
      save: false, // if true simulation is saved and shows up in the dashboard
      save_if_fails: true, // if true, reverting simulations show up in the dashboard
      simulation_type: 'full', // full or quick
      // block_header: null, // block header override
      // network to simulate on
      network_id: '1',
      // simulate transaction at this (historical) block number
      block_number: 16527769,
      // simulate transaction at this index within the (historical) block
      transaction_index: 42,
      from: '0x1cf5cd427d0a968379bd6b5befce28d8e157ae38',
      input:
        '0x8803dbee0000000000000000000000000000000000000000000000b34dcb21540828000000000000000000000000000000000000000000000000000000000000dea6e4cd00000000000000000000000000000000000000000000000000000000000000a00000000000000000000000001cf5cd427d0a968379bd6b5befce28d8e157ae380000000000000000000000000000000000000000000000000000000063d93b620000000000000000000000000000000000000000000000000000000000000002000000000000000000000000dac17f958d2ee523a2206206994597c13d831ec70000000000000000000000007659ce147d0e714454073a5dd7003544234b6aa0',
      to: '0x7a250d5630b4cf539739df2c5dacb4c659f2488d',
      gas: 138864,
      gas_price: '32909736476',
      value: '0',
      access_list: [],
      generate_access_list: true,
    },
    {
      headers: {
        'X-Access-Key': TENDERLY_ACCESS_KEY as string,
      },
    }
  );

  // access the transaction object
  const transcation = resp.data.transaction;

  // access the transaction call trace
  const callTrace = transcation.transaction_info.call_trace;

  // access transaction's logs
  const logs = resp.data.transaction.transaction_info.logs;

  console.log(
    `Simulated transaction info: \nhash: ${transcation.hash} \nblock number: ${transcation.block_number}`
  );

  // display balance changes
  console.log(
    'Balance changes',
    '\n\t' +
      callTrace.balance_diff
        .map(
          (balance: any) =>
            `${balance.address}: ${balance.original} -> ${balance.dirty} ${
              balance.is_miner ? '(Miner)' : ''
            }`
        )
        .join('\n\t')
  );

  // display output values
  console.log(
    'Output values' +
      '\n\t' +
      callTrace.decoded_output
        .map(
          (output: any) =>
            `${output.soltype.name} ${output.soltype.type} = ${JSON.stringify(
              output.value
            )}`
        )
        .join('\n\t')
  );

  // display events
  console.log(
    'Events' +
      '\n\t' +
      logs
        .map(
          (log: any) =>
            `${log.name} (${log.inputs
              .map(
                (input: any) =>
                  `${input.soltype.name} ${input.soltype.type} = ${input.value}`
              )
              .join(', ')})`
        )
        .join('\n\t')
  );

  const stateDiff = resp.data.transaction.transaction_info.state_diff;

  // display state changes for all affected contracts
  console.log(
    'State changes' +
      '\n\t' +
      stateDiff
        .map(
          (diff: any) =>
            `${diff.address}
${diff.soltype.name}: ${diff.soltype.type}
  ${JSON.stringify(diff.original)} -> ${JSON.stringify(diff.dirty)}
  `
        )
        .join('\n\t')
  );
};

simulateUniswap();

```
````
{% endcode %}

The output shows something similar to this:

````

Simulated transaction info: 
hash: 0x0b7e58d70c730b97c02867ec589192d774d48569b823f85c679599d019341ebe 
block number: 16527769

Balance changes 
	0x1cf5cd427d0a968379BD6b5BefcE28d8e157AE38: 178649986537506409 -> 175016718720819533 
	0xC0E1b256DE232262134c22f73b21F756072Bfb73: 4913764247259774380 -> 4913874657421732568 (Miner)
Output values
	amounts uint256[] = ["3731747754","3307572800000000262144"]
Events
	Transfer (from address = 0x1cf5cd427d0a968379bd6b5befce28d8e157ae38, to address = 0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a, value uint256 = 3731747754)
	Transfer (from address = 0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a, to address = 0x1cf5cd427d0a968379bd6b5befce28d8e157ae38, value uint256 = 3307572800000000262144)
	Sync (reserve0 uint112 = 253974535984473723669255, reserve1 uint112 = 289417250282)
	Swap (sender address = 0x7a250d5630b4cf539739df2c5dacb4c659f2488d, amount0In uint256 = 0, amount1In uint256 = 3731747754, amount0Out uint256 = 3307572800000000262144, amount1Out uint256 = 0, to address = 0x1cf5cd427d0a968379bd6b5befce28d8e157ae38)
State changes
	0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a
reserve1: uint112
  "285685502528" -> "289417250282"
  
	0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a
reserve0: uint112
  "257282108784473723931399" -> "253974535984473723669255"
  
	0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a
blockTimestampLast: uint32
  "0" -> "0"
  
	0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a
price0CumulativeLast: uint256
  "756643269219333625014234830491" -> "756717575180654871536825733691"
  
	0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a
price1CumulativeLast: uint256
  "115330660026005862214326453602290190379962570339216427" -> "115390925201612227497765383158300036629651585476758491"
  
	0x7659ce147d0e714454073a5dd7003544234b6aa0
_balances: mapping (address => uint256)
  {"0x1cf5cd427d0a968379bd6b5befce28d8e157ae38":"13735118200000000589824","0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a":"257282108784473723931399"} -> {"0x1cf5cd427d0a968379bd6b5befce28d8e157ae38":"17042691000000000851968","0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a":"253974535984473723669255"}
  
	0xdac17f958d2ee523a2206206994597c13d831ec7
balances: mapping (address => uint256)
  {"0x1cf5cd427d0a968379bd6b5befce28d8e157ae38":"22963773121","0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a":"285685502528"} -> {"0x1cf5cd427d0a968379bd6b5befce28d8e157ae38":"19232025367","0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a":"289417250282"}
```
````

{% hint style="info" %}
When transactions are simulated via API, by default they don’t get persisted. To help the debugging using the Dashboard, you can configure `save_if_fails` flag. If you need to persist the transaction in case of success too, you can set `save` flag to `true`. Both of these are `false` by default.
{% endhint %}

{% hint style="info" %}
Transactions are executed by default in `full` mode. To speed up simulations even further, you can set `simulation_type` to `quick`. Full simulations use the source code of the smart contract to generate call traces, whereas quick simulations use only the bytecode and thus take less time.
{% endhint %}

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
