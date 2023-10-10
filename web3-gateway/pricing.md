---
description: >-
  Tenderly Node usage and rate-limiting are expressed in Tenderly Units (TU).
  Read, write, compute, and advanced compute requests contribute with different
  weights to the total.
---

# Pricing and usage limits

Tenderly Node usage is measured with respect to requests your dapp makes to the Tenderly Node JSON RPC. The requests are divided into three categories, each having a different usage footprint, measured in **Tenderly Units** (**TU**):&#x20;

**Read (1 TU)**

**Write (20 TU)**

**Compute (4 TU)**

**Advanced** **Compute (400 TU)**

To calculate the usage over a period of time, you need to multiply the number of requests by the usage footprint of the request category. For example, if your dapp makes 1000 read requests and 100 write requests, the usage is:

```
1000 * 1 TU + 100 * 20 TU = 3000 TU
```

| Category             | Description                                                                             | Usage footprint |
| -------------------- | --------------------------------------------------------------------------------------- | --------------- |
| **Read**             | Read-only requests, such as `eth_getBalance` or `eth_getTransactionByHash`              | **1 TU**        |
| **Write**            | Write requests, such as `eth_sendTransaction` or `eth_sendRawTransaction`               | **20 TU**       |
| **Compute**          | Compute requests, such as `eth_call` or `eth_estimateGas`                               | **4 TU**        |
| **Advanced Compute** | Compute requests, such as `tenderly_simulateTransaction` or `tenderly_traceTransaction` | **400 TU**      |

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
* `tenderly_traceTransaction`
* `tenderly_simulateBundle` (multiplied by the number of transactions in a bundle)

</details>

### Usage rate limiting and monthly quota

Depending on your plan, you'll have the monthly quota and usage rate limiting shown in the following table.

| Parameter/plan | Free          | Starter       |
| -------------- | ------------- | ------------- |
| Monthly quota  | 25.000.000 TU | 35.000.000 TU |
| Rate Limit     | 10 TU/s       | 20 TU/s       |
| Price          | -             | $50           |

{% hint style="info" %}
All RPC endpoints are included in Free, Dev, and Pro plans.&#x20;

For Free and Starter plans, higher rate limits are likely to be observed compared to the ones listed below.
{% endhint %}
