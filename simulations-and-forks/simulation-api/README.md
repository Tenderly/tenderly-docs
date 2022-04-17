# Simulation API

## Overview

The simulator enables you to seamlessly fork the chain and simulate the execution of any transactions as if time has frozen. You can fork (aka stop) any network at any block. This can help you validate any hypothesis you have, ranging from understanding how smart contract logic is behaving in some specific environment setup to creating the whole “sandbox” environment of the network.

Here are some examples of what you can achieve:

* Dry-run user transactions, saving them money on failed transactions and improving UX.
* DApp playground mode - Let users try out your dApp without spending any gas with all production data readily available.
* Staging and QA environments for a blockchain project.
* CI/CD for your blockchain project.
* Validating complex DAO governance proposals.

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

We can start with a single simulation that is not recording any state. You can see the output of the transaction, if it failed or not, without actually sending it to the chain and spending gas. You can simulate any transaction using any given contract deployed on networks available in Tenderly.

Let’s execute a simple ERC20 transfer simulation on the DAI contract.

**API Typescript**

```tsx
dotenv.config(); // load environment variables using dotenv 

const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;
const SIMULATE_URL = `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/simulate`

// set up your access-key, if you don't have one or you want to generate new one follow next link
// https://dashboard.tenderly.co/account/authorization
const opts = {
    headers: {
        'X-Access-Key': TENDERLY_ACCESS_KEY as string,
  }
}

const body = {
  // standard TX fields
  "network_id": "1",
  "from": senderAddr,
  "to": contract.address,
  "input": unsignedTx.data,
  "gas": 21204,
  "gas_price": "0",
  "value": 0,
	// simulation config (tenderly specific)
	"save_if_fails": true,
  "save": false,
	"simulation_type": "quick"
}

const resp = await axios.post(SIMULATE_URL, body, opts);
```

{% hint style="info" %}
When transactions are simulated via API, by default they don’t get persisted. To help the debugging using the Dashboard, you can configure `save_if_fails` flag. If you need to persist the transaction in case of success too, you can set `save` flag to `true`. Both of these are `false` by default.
{% endhint %}

{% hint style="info" %}
Transactions are executed by default in `full` mode. To speed up simulations even further, you can set `simulation_type` to `quick`. Full simulations use the source code of the smart contract to generate call traces, whereas quick simulations use only the bytecode and thus take less time.
{% endhint %}

### 2 Create a Fork environment

Next, after we have executed a one-off simulation let’s execute them together. We are going to execute them under the “forked” environment. You can imagine it as if time has stopped on a specific block and only we can execute simulated transactions that would apply to the desired chain.

Here we are going to fork Ethereum **Mainnet** on the **14386016** blocks:

**API Typescript**

```tsx
const TENDERLY_PROJECT = "project";
const TENDERLY_FORK_API = `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/simulate`

// set up your access-key, if you don't have one or you want to generate new one follow next link
// https://dashboard.tenderly.co/account/authorization
const opts = {
      headers: {
          'X-Access-Key': ACCESS_KEY,
    }
  }

const body = {
  "network_id": "1",
	"block_number": 14386016,
}

const resp = await axios.post(TENDERLY_FORK_API, body, opts);
```

#### 2.1 Using Fork with ethers.js

After creating a Tenderly Fork, you can interact with its JSON-RPC API, returned through `simulation_fork.rpc_url`. After, you can spawn ethers.js with any other network you are using or plan to use.

💡 Tenderly will create 10 test addresses with 100 ETH. By default, ethers.js will do transaction signing with the 0th address as the default signer.

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

Let’s see how we can mint new Ether to our test address. Here we’re using the custom Tenderly JSON-PRC endpoint `tenderly_addBalance`.

**API Typescript**

```tsx
const params = [
        [YOUR_WALLET_ADDRESS],
        ethers.utils.hexValue(100) // hex encoded wei amount
];

await provider.send('tenderly_addBalance', params)
```

### 4 Execute transaction in Tenderly Fork

Now that we have enough Ethers to cover all gas costs for our transactions. Let’s start to chain transaction simulations, we are going to execute `approve()` and `transferFrom()` functions on top of the DAI contract. But before we do, we are going to `transfer()` some tokens to our default Signer address.

We can use the provider we have created in 2.1 with ethers.js.

**API Typescript**

```tsx
const DAI_ADDRESS = "0x6B175474E89094C44Da98b954EedeAC495271d0F";
const DAI_ABI = "{...}";

const daiContract = new ethers.Contract(DAI_ADDRESS , DAI_ABI , signer);

// we can use ether encoding because dai contract has 18 decimals
const tokenAmount = utils.parseEther('1').toString(10);

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

await axios.delete(TENDERLY_FORK_ACCESS_URL), {}, opts)
```

{% hint style="success" %}
In the following articles you will find specific code examples in some places. If you want to browse our code repo immediately you can find it in [**this GitHub repo**](https://github.com/Tenderly/integration-samples).
{% endhint %}

{% hint style="info" %}
You can check out the [plans and pricing for the Simulation API here](../../other/simulation-api-rate-limits.md). You can also check out all [Public API endpoints here](https://docs-api.tenderly.co) - this documentation space is under continuous development, so if you need some API endpoints that aren't available or other API needs that aren't listed publicly, please ping us via [**Intercom on the Tenderly Dashboard**](https://dashboard.tenderly.co) **** and we'll do our best to meet your needs 🖖
{% endhint %}
