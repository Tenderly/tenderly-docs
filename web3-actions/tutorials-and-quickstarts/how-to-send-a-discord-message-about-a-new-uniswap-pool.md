---
description: >-
  Follow a step-by-step guide to create a Web3 Action that will send you a
  Discord message whenever a new Uniswap V3 pool is created.
---

# How to Send a Discord Message About a New Uniswap Pool

This tutorial shows you **how to use a Web3 Action to send a message to a Discord channel when a new pool is created on Uniswap V3**. You can use this Web3 Action to notify your community when something happens on the chain.

{% hint style="info" %}
The entire code is available in **** [**this Github repo**](https://github.com/Tenderly/examples-web3-actions/). Note that it’s in a separate branch at the moment.
{% endhint %}

## Project Overview

The goal of this project is to teach you how to use Web3 Actions to send a Discord message whenever a Uniswap Pool is made. We’ll show you two approaches - the more convenient one is to use <mark style="color:orange;">`PoolCreated`</mark> event as a trigger for our Web3 Action (see the **** [**Uniswap docs**](https://docs.uniswap.org/protocol/V2/reference/smart-contracts/factory#paircreated)).

## The Plan

* Add contracts to your Tenderly project - [**UniswapV3ContractFactory**](https://dashboard.tenderly.co/nenad/uniswap/contract/mainnet/0x1f98431c8ad98523631ae4a59f267346ea31f984). It’s already verified and present in Tenderly, so you just need to add them to your project.
* Store the Discord Webhook URL in your Web3 Action Secrets.
* Create a Web3 Action that will respond to the <mark style="color:orange;">`[PoolCreated](<https://docs.uniswap.org/protocol/reference/core/interfaces/IUniswapV3Factory#poolcreated>)`</mark>event.

### 1: Add Uniswap Contracts to Your Tenderly Project

Web3 Actions require that smart contracts used to specify triggers are verified in Tenderly.

Web3 Actions require that smart contracts used to specify triggers are verified in Tenderly. Since we’re using existing contracts, you can find them using the search bar by typing in the contract name or address.

Alternatively, go to **** [**UniswapV2ContractFactory**](https://dashboard.tenderly.co/contract/mainnet/0x5c69bee701ef814a2b6a3edd4b1652cb9cc5aa6f) and click **“Add to Project”**. Do the same for [**UniswapV2Pair**](https://dashboard.tenderly.co/contract/mainnet/0xd849b2af570ffa3033973ea11be6e01b7ba661d9).

### 2: Create a Web3 Action for the PoolCreated Event

Below you’ll find the code for our Web3 Action as well as an explanation of how it works:

```typescript
import {
	ActionFn,
	Context,
	Event,
	TransactionEvent,
} from '@tenderly/actions'
import axios from 'axios';
import { ethers } from 'ethers';

import UniswapV3FactoryAbi from './UniswapV3FactoryAbi.json'

export const onPoolCreatedEventEmitted: ActionFn = async (context: Context, event: Event) => {
	try {
		const txEvent = event as TransactionEvent;

		const eventLog = await getPoolCreatedEvent(txEvent);

		const tokensData = await getTokensData(eventLog.token0, eventLog.token1);
		console.log("Received Tokens Data: ", tokensData);

		await notifyDiscord(`${tokensData.token0.name} ↔️ ${tokensData.token1.name}`, context);

	} catch (error) {
		console.error(error);
	}
}

const getPoolCreatedEvent = async (txEvent: TransactionEvent) => {
	const ifc = new ethers.utils.Interface(UniswapV3FactoryAbi);
	const poolCreatedTopic = ifc.getEventTopic("PoolCreated");

	const poolCreatedEventLog = txEvent.logs.find(log => {
		return log.topics.find(topic => topic == poolCreatedTopic) !== undefined
	})

	if (poolCreatedEventLog == undefined) {
		throw Error("PoolCreatedEvent missing")
	}
	return ifc.decodeEventLog("PoolCreated",
		poolCreatedEventLog.data,
		poolCreatedEventLog.topics) as unknown as UniswapPool;
}

const getTokensData = async (token0: string, token1: string) => {
	const tokenFields = `id, name, symbol, totalValueLocked, totalSupply, derivedETH`;
	const theGraphQuery = `
{
	token0: token(id:"${token0.toLowerCase()}"){${tokenFields}},
	token1: token(id:"${token1.toLowerCase()}"){${tokenFields}}
}`;

	const UNISWAP_THE_GRAPH = "https://api.thegraph.com/subgraphs/name/uniswap/uniswap-v3";
	const resp = await axios.post(UNISWAP_THE_GRAPH, {
		query: theGraphQuery
	});

	return resp.data.data as unknown as {
		token0: UniwswapToken,
		token1: UniwswapToken
	}
}

const notifyDiscord = async (text: string, context: Context) => {
	console.log('Sending to Discord:', `🐥 ${text}`)
	const webhookLink = await context.secrets.get("discord.uniswapChannelWebhook");
	await axios.post(
		webhookLink,
		{
			'content': `🐥 ${text}`
		},
		{
			headers: {
				'Accept': 'application/json',
				'Content-Type': 'application/json'
			}
		}
	);

}

type UniswapPool = {
	token0: string,
	token1: string,
	fee: number,
	tickSpacing: number,
	pool: number
}

type UniwswapToken = {
	id: string,
	name: string,
	symbol: string,
	tokenValueLocked: number,
	totalSupply: number,
	derivedEth: number
}
```

**Obtain Tokens in the Newly Created Pool.** To get information about two tokens in the new pool, we need to search through the transaction logs in the <mark style="color:orange;">`getEventLog`</mark> function. We’re using Ethers and the ABI of the contract: <mark style="color:orange;">`UniswapV3FactoryAbi`</mark>. Go to the <mark style="color:orange;">`UniswapV3Factory`</mark> [**contract in Tenderly**](https://dashboard.tenderly.co/nenad/uniswap/contract/mainnet/0x1f98431c8ad98523631ae4a59f267346ea31f984), click **“View ABI”** and copy/paste it to a local file in the <mark style="color:orange;">`actions`</mark> directory.

Essentially, we’re looking for the log entry in the topic <mark style="color:orange;">`PoolCreate`</mark>. First, we’re taking a reference of that topic (<mark style="color:orange;">`poolCreatedTopic = ifc.getEventTopic("PoolCreated")`</mark>) and then we’re filtering the actual logs (<mark style="color:orange;">`tx.logs`</mark>) until we find the entry referencing that topic. Lastly, we’re decoding the log we found (<mark style="color:orange;">`poolCreatedEventLog`</mark>) using Ethers. This is the event we’re looking for, and it contains the addresses of the tokens: <mark style="color:orange;">`token0`</mark> and <mark style="color:orange;">`token1`</mark>.

**Obtain Token Data Using Uniswap’s Graph API on TheGraph.** Uniswap exposes access to its data through **** [**TheGraph**](https://thegraph.com/hosted-service/subgraph/uniswap/uniswap-v3). We’re using the <mark style="color:orange;">`getTokensData`</mark> function to query TheGraph and get several fields for the <mark style="color:orange;">`token0`</mark> and <mark style="color:orange;">`token1`</mark> IDs – the ones present in the <mark style="color:orange;">`PoolCreated`</mark> event from the first step.

**Notify the Discord Community.** Having gathered all the relevant information, we are ready to send a message to our Discord channel. With the <mark style="color:orange;">`notifyDiscord`</mark> function, we need to get the Webhook URL from the <mark style="color:orange;">`secrets`</mark>. We’re using Axios to make an HTTP post request to run the Webhook and pass the content.

### 3: Configure Your Web3 Action

In the <mark style="color:orange;">`tenderly.yaml`</mark> file, we’re need to specify that we want to have <mark style="color:orange;">`uniswapActions:onPoolCreatedEventEmitted`</mark> ran when an event is fired from the <mark style="color:orange;">`UniswapV3Factory`</mark> contract (on address <mark style="color:orange;">`0xd849b2af570ffa3033973ea11be6e01b7ba661d9`</mark>) within a transaction that is mined on the Mainnet (network 1).

```yaml
account_id: ""
actions:
  YOUR_USERNAME/YOUR_PROJECT_SLUG:
    runtime: v1
    sources: actions
    specs:
      uniswapNewPool:
        description: Runs when a new swap is made on Uniswap
        function: uniswapActions:onPoolCreatedEventEmitted
        trigger:
          type: transaction
          transaction:
            status:
              - mined
            filters:
              - network: 1
                eventEmitted: 
                  contract: 
                    address: 0xd849b2af570ffa3033973ea11be6e01b7ba661d9
                  name: PoolCreated
project_slug: ""
```

### 4: Store the Discord Webhook URL in Secrets

Before running our Web3 Action in Tenderly, we have to set the value for the Discord Webhook.

In the Tenderly Dashboard, go to the Actions page of your project and click Secrets. Add a new secret named <mark style="color:orange;">`discord.uniswapChannelWebhook`</mark> and paste your Discord channel’s Webhook.

### 5: Deploy and Try Out Your Web3 Action

Deploy your Web3 Action by running this command:

```yaml
tenderly actions deploy
```

**To try out if your Web3 Action is working, go to the Actions page in your Tenderly Dashboard. Select your Action and click Manual Trigger.**

That’s all! Hopefully, you’ve received a message on your Discord channel 🎉
