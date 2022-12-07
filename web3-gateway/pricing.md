---
description: >-
  The Web3 Gateway usage and rate-limiting is expressed in Tenderly Units (TU),
  while read, write, compute and advanced compute requests contribute with
  different weights to the total.
---

# Pricing and usage limits

Web3 Gateway usage is measured with respect to requests your dapp makes to the Web3 Gateway JSON RPC. The requests are divided into three categories, each having different usage footprint, measured in **Tenderly Units** (**TU**): **Read (1 TU)**, **Write (20 TU)**, **Compute (4 TU)** and **Advanced** **Compute (40 TU)**,

To calculate the usage over a period of time, you need to multiply the number of requests by the usage footprint of the request category. For example, if your dapp makes 1000 read requests and 100 write requests, the usage is:

```
1000 * 1 TU + 100 * 20 TU = 3000 TU
```

| Category             | Description                                                                 | Usage footprint |
| -------------------- | --------------------------------------------------------------------------- | --------------- |
| **Read**             | Read-only requests, such as `eth_getBalance` or `eth_getTransactionByHash`. | **1 TU**        |
| **Write**            | Write requests, such as `eth_sendTransaction` or `eth_sendRawTransaction`.  | **20 TU**       |
| **Compute**          | Compute requests, such as `eth_call` or `eth_estimateGas`.                  | **4 TU**        |
| **Advanced Compute** | Compute requests, such as `tenderly_simulateTransaction`.                   | **40 TU**       |

<details>

<summary>Read Methods</summary>

* `eth_accounts`
* `eth_blockNumber`
* `eth_chainId`
* `eth_coinbase`
* `eth_feeHistory`
* `eth_gasPrice`
* `eth_getBalance`
* `eth_getBlockByHash`
* `eth_getBlockByNumber`
* `eth_getBlockReceipts`
* `eth_getBlockTransactionCountByHash`
* `eth_getBlockTransactionCountByNumber`
* `eth_getCode`
* `eth_getStorageAt`
* `eth_getTransactionByBlockHashAndIndex`
* `eth_getTransactionByBlockNumberAndIndex`
* `eth_getTransactionByHash`
* `eth_getTransactionCount`
* `eth_getTransactionReceipt`
* `eth_getUncleByBlockHashAndIndex`
* `eth_getUncleByBlockNumberAndIndex`
* `eth_getUncleCountByBlockHash`
* `eth_getUncleCountByBlockNumber`
* `eth_hashrate`
* `eth_maxPriorityFeePerGas`
* `eth_mining`
* `eth_newBlockFilter`
* `eth_newFilter`
* `eth_protocolVersion`
* `eth_syncing`
* `eth_uninstallFilter`
* `net_listening`
* `net_peerCount`
* `net_version`
* `web3_clientVersion`
* `web3_sha3`

</details>

<details>

<summary>Compute Methods</summary>

* `eth_call`
* `eth_estimateGas`
* `eth_getFilterChanges`
* `eth_getFilterLogs`
* `eth_getLogs`

</details>

<details>

<summary>Write Methods</summary>

* `eth_sendRawTransaction`

</details>

<details>

<summary>Advanced Compute Methods</summary>

* `tenderly_simulateTransaction`

</details>

### Usage rate limiting and monthly quota

Depending on your plan, you'll have the monthly quota and usage rate limiting shown in the table below.

{% hint style="info" %}
All RPC endpoints are included Free, Dev, Pro and Early Adopters plans.&#x20;

For Free, Dev and Pro plans higher rate limits are likely to be observed.
{% endhint %}

| Parameter\plan | Free/Dev/Pro         | Early Adopters |
| -------------- | -------------------- | -------------- |
| Monthly quota  | 25.000.000 TU        | 100.000.000 TU |
| Rate Limit     | 20 TU/s              | 60 TU/s        |
| Price          | included in the plan | $50            |
