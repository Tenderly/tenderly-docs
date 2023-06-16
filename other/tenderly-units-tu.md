---
description: >-
  Tenderly Units - the measure of computational resources consumption on the
  Tenderly full-stack node.
---

# ⛽ Tenderly Units (TU)

Tenderly units represent a measure of the total computational resources your applications are consuming on Tenderly.&#x20;

Tenderly units are similar to how you would be charged by platforms like Google Cloud Platform (GCP) or Amazon Web Services (AWS) for the computing resources used. Operations performed on the Tenderly platform are assigned a certain quantity of Tenderly Units (TU), and are executed within the rate limit permitted by your billing plan.

### **Pricing Plans**

| Parameter/plan | Free                 | Starter       | Custom |
| -------------- | -------------------- | ------------- | ------ |
| Monthly quota  | 25.000.000 TU        | 35.000.000 TU | Custom |
| Rate Limit     | 10 TU/s              | 20 TU/s       | Custom |
| Price          | included in the plan | $50           | Custom |

## **Tenderly Units (TU) cost**

#### **Web3Gateway**

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

#### **Web3Actions**

| Description           | Usage footprint |
| --------------------- | --------------- |
| Scanned Transaction   | **40 TU**       |
| Action Execution (ms) | **1 TU**        |
| Action Invocation     | **50 TU**       |
| Active Action         | **2 TU/sec**    |

#### **Alerting & Monitoring**

| Description         | Usage footprint |
| ------------------- | --------------- |
| Scanned Transaction | **40 TU**       |
| Action Dispatched   | **50 TU**       |
| Active Alert Rule   | **2 TU/sec**    |
