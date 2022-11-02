---
description: >-
  A brief overview of supported Ethereum JSON RPC calls.
---

{% hint style='info'%}
This page shows a brief overview of supported Ethereum JSON RPC calls.
Find a [detaild list of supported calls](detailed-json-rpc.md).
{% hint %}

## `eth_getBlockByHash`

Returns information about a block by hash.

[Detailed version](./detailed-json-rpc.md#eth_getBlockByHash)

**RESULT**: Block information

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockByHash",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    false
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockByHash",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    false
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetBlockByHash() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getBlockByHash(
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    false
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetBlockByHash();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getBlockByNumber`

Returns information about a block by number.

[Detailed version](./detailed-json-rpc.md#eth_getBlockByNumber)

**RESULT**: Block information

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockByNumber",
  "params": ["latest", false]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockByNumber",
  "params": [
    "latest",
    false
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetBlockByNumber() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getBlockByNumber("latest", false);

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetBlockByNumber();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getBlockTransactionCountByHash`

Returns the number of transactions in a block from a block matching the given block hash.

[Detailed version](./detailed-json-rpc.md#eth_getBlockTransactionCountByHash)

**RESULT**: Transaction count

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockTransactionCountByHash",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockTransactionCountByHash",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetBlockTransactionCountByHash() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getBlockTransactionCountByHash(
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetBlockTransactionCountByHash();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getBlockTransactionCountByNumber`

Returns the number of transactions in a block matching the given block number.

[Detailed version](./detailed-json-rpc.md#eth_getBlockTransactionCountByNumber)

**RESULT**: Transaction count

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockTransactionCountByNumber",
  "params": ["latest"]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBlockTransactionCountByNumber",
  "params": [
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetBlockTransactionCountByNumber() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getBlockTransactionCountByNumber("latest");

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetBlockTransactionCountByNumber();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getUncleCountByBlockHash`

Returns the number of uncles in a block from a block matching the given block hash.

[Detailed version](./detailed-json-rpc.md#eth_getUncleCountByBlockHash)

**RESULT**: Uncle count

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getUncleCountByBlockHash",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getUncleCountByBlockHash",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetUncleCountByBlockHash() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getUncleCountByBlockHash(
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetUncleCountByBlockHash();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getUncleCountByBlockNumber`

Returns the number of transactions in a block matching the given block number.

[Detailed version](./detailed-json-rpc.md#eth_getUncleCountByBlockNumber)

**RESULT**: Uncle count

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getUncleCountByBlockNumber",
  "params": ["latest"]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getUncleCountByBlockNumber",
  "params": [
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetUncleCountByBlockNumber() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getUncleCountByBlockNumber("latest");

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetUncleCountByBlockNumber();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_chainId`

Returns the chain ID of the current network.

[Detailed version](./detailed-json-rpc.md#eth_chainId)

**RESULT**: Chain ID

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_chainId",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_chainId",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runChainId() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_chainId();

  // Print the output to console
  console.log(result);
}

(async () => {
  runChainId();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_syncing`

Returns an object with data about the sync status or false.

[Detailed version](./detailed-json-rpc.md#eth_syncing)

**RESULT**: Syncing status

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_syncing",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_syncing",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runSyncing() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_syncing();

  // Print the output to console
  console.log(result);
}

(async () => {
  runSyncing();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_accounts`

Returns a list of addresses owned by client.

[Detailed version](./detailed-json-rpc.md#eth_accounts)

**RESULT**: Accounts

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_accounts",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_accounts",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runAccounts() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_accounts();

  // Print the output to console
  console.log(result);
}

(async () => {
  runAccounts();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_blockNumber`

Returns the number of most recent block.

[Detailed version](./detailed-json-rpc.md#eth_blockNumber)

**RESULT**: Block number

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_blockNumber",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_blockNumber",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runBlockNumber() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_blockNumber();

  // Print the output to console
  console.log(result);
}

(async () => {
  runBlockNumber();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_call`

Executes a new message call immediately without creating a transaction on the block chain.

[Detailed version](./detailed-json-rpc.md#eth_call)

**RESULT**: Return data

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_call",
  "params": [
    {
      "from": "0x4469880099472dddfd357ab305ad2821d6e4647f",
      "to": "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      "gas": "0x4e3b29200",
      "gasPrice": "0x89d12e6c0",
      "value": "0x258689ac70a8000",
      "data": "0x"
    },
    "latest"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_call",
  "params": [
    {
      "from": "0x4469880099472dddfd357ab305ad2821d6e4647f",
      "to": "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      "gas": "0x4e3b29200",
      "gasPrice": "0x89d12e6c0",
      "value": "0x258689ac70a8000",
      "data": "0x"
    },
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runCall() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_call(
    {
      from: "0x4469880099472dddfd357ab305ad2821d6e4647f",
      to: "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      gas: "0x4e3b29200",
      gasPrice: "0x89d12e6c0",
      value: "0x258689ac70a8000",
      data: "0x",
    },
    "latest"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runCall();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_estimateGas`

Generates and returns an estimate of how much gas is necessary to allow the transaction to complete.

[Detailed version](./detailed-json-rpc.md#eth_estimateGas)

**RESULT**: Gas used

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_estimateGas",
  "params": [
    {
      "from": "0x4469880099472dddfd357ab305ad2821d6e4647f",
      "to": "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      "gas": "0x4e3b29200",
      "gasPrice": "0x89d12e6c0",
      "value": "0x258689ac70a8000",
      "data": "0x"
    },
    "latest"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_estimateGas",
  "params": [
    {
      "from": "0x4469880099472dddfd357ab305ad2821d6e4647f",
      "to": "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      "gas": "0x4e3b29200",
      "gasPrice": "0x89d12e6c0",
      "value": "0x258689ac70a8000",
      "data": "0x"
    },
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runEstimateGas() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_estimateGas(
    {
      from: "0x4469880099472dddfd357ab305ad2821d6e4647f",
      to: "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      gas: "0x4e3b29200",
      gasPrice: "0x89d12e6c0",
      value: "0x258689ac70a8000",
      data: "0x",
    },
    "latest"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runEstimateGas();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_gasPrice`

Returns the current price per gas in wei.

[Detailed version](./detailed-json-rpc.md#eth_gasPrice)

**RESULT**: Gas price

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_gasPrice",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_gasPrice",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGasPrice() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_gasPrice();

  // Print the output to console
  console.log(result);
}

(async () => {
  runGasPrice();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_maxPriorityFeePerGas`

Returns the current maxPriorityFeePerGas per gas in wei.

[Detailed version](./detailed-json-rpc.md#eth_maxPriorityFeePerGas)

**RESULT**: Max priority fee per gas

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_maxPriorityFeePerGas",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_maxPriorityFeePerGas",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runMaxPriorityFeePerGas() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_maxPriorityFeePerGas();

  // Print the output to console
  console.log(result);
}

(async () => {
  runMaxPriorityFeePerGas();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_feeHistory`

Transaction fee history

[Detailed version](./detailed-json-rpc.md#eth_feeHistory)

**RESULT**: feeHistoryResult
Fee history for the returned block range. This can be a subsection of the requested range if not all blocks are available.
{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_feeHistory",
  "params": [2, "latest", []]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_feeHistory",
  "params": [
    2,
    "latest",
    []
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runFeeHistory() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_feeHistory(2, "latest", []);

  // Print the output to console
  console.log(result);
}

(async () => {
  runFeeHistory();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_newFilter`

Creates a filter object, based on filter options, to notify when the state changes (logs).

[Detailed version](./detailed-json-rpc.md#eth_newFilter)

**RESULT**: Filter Identifier

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_newFilter",
  "params": [null]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_newFilter",
  "params": [
    null
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runNewFilter() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_newFilter();

  // Print the output to console
  console.log(result);
}

(async () => {
  runNewFilter();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_newBlockFilter`

Creates a filter in the node, to notify when a new block arrives.

[Detailed version](./detailed-json-rpc.md#eth_newBlockFilter)

**RESULT**: Filter Identifier

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_newBlockFilter",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_newBlockFilter",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runNewBlockFilter() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_newBlockFilter();

  // Print the output to console
  console.log(result);
}

(async () => {
  runNewBlockFilter();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_uninstallFilter`

Uninstalls a filter with given id.

[Detailed version](./detailed-json-rpc.md#eth_uninstallFilter)

**RESULT**: Success

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_uninstallFilter",
  "params": [null]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_uninstallFilter",
  "params": [
    null
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runUninstallFilter() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_uninstallFilter();

  // Print the output to console
  console.log(result);
}

(async () => {
  runUninstallFilter();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getFilterChanges`

Polling method for a filter, which returns an array of logs which occurred since last poll.

[Detailed version](./detailed-json-rpc.md#eth_getFilterChanges)

**RESULT**: Log objects

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getFilterChanges",
  "params": [null]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getFilterChanges",
  "params": [
    null
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetFilterChanges() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getFilterChanges();

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetFilterChanges();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getFilterLogs`

Returns an array of all logs matching filter with given id.

[Detailed version](./detailed-json-rpc.md#eth_getFilterLogs)

**RESULT**: Log objects

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getFilterLogs",
  "params": [null]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getFilterLogs",
  "params": [
    null
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetFilterLogs() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getFilterLogs();

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetFilterLogs();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getLogs`

Returns an array of all logs matching filter with given id.

[Detailed version](./detailed-json-rpc.md#eth_getLogs)

**RESULT**: Log objects

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getLogs",
  "params": [null]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getLogs",
  "params": [
    null
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetLogs() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getLogs();

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetLogs();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_mining`

Returns whether the client is actively mining new blocks.

[Detailed version](./detailed-json-rpc.md#eth_mining)

**RESULT**: Mining status

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_mining",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_mining",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runMining() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_mining();

  // Print the output to console
  console.log(result);
}

(async () => {
  runMining();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_hashrate`

Returns the number of hashes per second that the node is mining with.

[Detailed version](./detailed-json-rpc.md#eth_hashrate)

**RESULT**: Mining status

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_hashrate",
  "params": []
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_hashrate",
  "params": []
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runHashrate() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_hashrate();

  // Print the output to console
  console.log(result);
}

(async () => {
  runHashrate();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getBalance`

Returns the balance of the account of given address.

[Detailed version](./detailed-json-rpc.md#eth_getBalance)

**RESULT**: Balance

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBalance",
  "params": ["0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b", "latest"]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getBalance",
  "params": [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetBalance() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getBalance(
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetBalance();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getStorageAt`

Returns the value from a storage position at a given address.

[Detailed version](./detailed-json-rpc.md#eth_getStorageAt)

**RESULT**: Value

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getStorageAt",
  "params": [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "0x0000000000000000000000000000000000000000000000000000000000000001",
    "latest"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getStorageAt",
  "params": [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "0x0000000000000000000000000000000000000000000000000000000000000001",
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetStorageAt() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getStorageAt(
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "0x0000000000000000000000000000000000000000000000000000000000000001",
    "latest"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetStorageAt();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getTransactionCount`

Returns the number of transactions sent from an address.

[Detailed version](./detailed-json-rpc.md#eth_getTransactionCount)

**RESULT**: Transaction count

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionCount",
  "params": ["0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b", "latest"]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionCount",
  "params": [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetTransactionCount() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getTransactionCount(
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetTransactionCount();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getCode`

Returns code at a given address.

[Detailed version](./detailed-json-rpc.md#eth_getCode)

**RESULT**: Bytecode

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getCode",
  "params": ["0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b", "latest"]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getCode",
  "params": [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetCode() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getCode(
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetCode();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_sendRawTransaction`

Submits a raw transaction.

[Detailed version](./detailed-json-rpc.md#eth_sendRawTransaction)

**RESULT**: Transaction hash

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_sendRawTransaction",
  "params": [
    {
      "from": "0x4469880099472dddfd357ab305ad2821d6e4647f",
      "to": "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      "gas": "0x4e3b29200",
      "gasPrice": "0x89d12e6c0",
      "value": "0x258689ac70a8000",
      "data": "0x"
    }
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_sendRawTransaction",
  "params": [
    {
      "from": "0x4469880099472dddfd357ab305ad2821d6e4647f",
      "to": "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
      "gas": "0x4e3b29200",
      "gasPrice": "0x89d12e6c0",
      "value": "0x258689ac70a8000",
      "data": "0x"
    }
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runSendRawTransaction() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_sendRawTransaction({
    from: "0x4469880099472dddfd357ab305ad2821d6e4647f",
    to: "0x4d97fa219bd42f42740659ca77d14e67d9eed7e4",
    gas: "0x4e3b29200",
    gasPrice: "0x89d12e6c0",
    value: "0x258689ac70a8000",
    data: "0x",
  });

  // Print the output to console
  console.log(result);
}

(async () => {
  runSendRawTransaction();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getTransactionByHash`

Returns the information about a transaction requested by transaction hash.

[Detailed version](./detailed-json-rpc.md#eth_getTransactionByHash)

**RESULT**: Transaction information

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByHash",
  "params": [
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByHash",
  "params": [
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetTransactionByHash() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getTransactionByHash(
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetTransactionByHash();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getTransactionByBlockHashAndIndex`

Returns information about a transaction by block hash and transaction index position.

[Detailed version](./detailed-json-rpc.md#eth_getTransactionByBlockHashAndIndex)

**RESULT**: Transaction information

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByBlockHashAndIndex",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    "0x1"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByBlockHashAndIndex",
  "params": [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    "0x1"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetTransactionByBlockHashAndIndex() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getTransactionByBlockHashAndIndex(
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    "0x1"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetTransactionByBlockHashAndIndex();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getTransactionByBlockNumberAndIndex`

Returns information about a transaction by block number and transaction index position.

[Detailed version](./detailed-json-rpc.md#eth_getTransactionByBlockNumberAndIndex)

**RESULT**: Transaction information

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByBlockNumberAndIndex",
  "params": ["latest", "0x1"]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionByBlockNumberAndIndex",
  "params": [
    "latest",
    "0x1"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetTransactionByBlockNumberAndIndex() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getTransactionByBlockNumberAndIndex(
    "latest",
    "0x1"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetTransactionByBlockNumberAndIndex();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}

## `eth_getTransactionReceipt`

Returns the receipt of a transaction by transaction hash.

[Detailed version](./detailed-json-rpc.md#eth_getTransactionReceipt)

**RESULT**: Receipt Information

{% tabs %}
{% tab title="Raw" %}

```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionReceipt",
  "params": [
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188"
  ]
}
```

{% endtab %}

{% tab title="cURL" %}

```bash

curl https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getTransactionReceipt",
  "params": [
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188"
  ]
}'

```

{% endtab %}

{% tab title="ethers" %}

```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runGetTransactionReceipt() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.eth_getTransactionReceipt(
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188"
  );

  // Print the output to console
  console.log(result);
}

(async () => {
  runGetTransactionReceipt();
})();
```

{% endtab %}

{% tab title="Response" %}

```json
N/A
```

{% endtab %}

{% endtabs %}
