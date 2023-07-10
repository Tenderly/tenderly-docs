---
description: Custom JSON RPC method available in Tenderly Web3 Gateway
---

# Simulate Bundle JSON RPC

{% hint style="info" %}
The custom RPC methods appear in the **`tenderly_`** namespace.
{% endhint %}

### `tenderly_simulateBundle`

Simulates a bundle of transactions as it would execute on the given block and returns results for each transaction.

**PARAMS**

1. **Transactions** Transactions `ARRAY`: list of transactions in a bundle
   * **from** (_optional_) `STRING`: hex encoded address
   * **to** `STRING`: hex encoded address
   * **gas** (_optional_) `NUMBER`
   * **maxFeePerGas** (_optional_) `NUMBER` max fee: The maximum total fee per gas the sender is willing to pay (includes the network / base fee and miner / priority fee) in wei
   * **maxPriorityFeePerGas** (_optional_) `NUMBER` max priority fee: Maximum fee per gas the sender is willing to pay to miners in wei
   * **gasPrice** (_optional_) `NUMBER`: The gas price willing to be paid by the sender in wei
   * **value** (_optional_) `NUMBER`
   * **data** (_optional_) `STRING`: hex encoded bytes
   * **accessList** (_optional_) `ARRAY` of Access list entry `OBJECT`
     * **address** `STRING` hex encoded address
     * **storageKeys** `ARRAY` of `STRING` representation of 32 byte hex encoded storage key
2. **Simulation Block Number** (_optional_) The block number against which transaction should be simulated. Either:
   * `STRING` Block number
   * `ENUM` of Block tag `earliest|finalized|safe|latest|pending`
3. **State Overrides** (_optional_) `MAP`: mapping from an account (address) to override specification
   * **key** `STRING`: the account this override applies to
   * **value** `OBJECT`: the override specification
     * **nonce** (_optional_) `STRING`: hex encoded 8 byte nonce override for the account
     * **code** (_optional_) `STRING`: data of the code override for the account
     * **balance** (_optional_) `STRING`: hex encoded 32 byte balance override for the account in wei
     * **stateDiff** (_optional_) `MAP`: mapping of storage key to storage value override
       * **key** `STRING`: the storage key
       * **value** `STRING`: the value override for the given storage key
4. &#x20;**Block Overrides** (optional) `OBJECT`: The set of header fields to override in a block.&#x20;
   * **number** _(optional)_ `STRING`: hex, overrides the block number
   * **difficulty** _(optional)_ `STRING`: hex, overrides the block difficulty
   * **time** (_optional_) `STRING`: hex, overrides block timestamp
   * **gasLimit** _(optional)_ `STRING`: hex, overrides gas limit
   * **coinbase** _(optional)_ `STRING`: hex, overrides block miner
   * **random** _(optional)_ `STRING`: hex, overrides the blocks extra data which feeds into the RANDOM opcode
   * **baseFee** _(optional)_ `STRING`: hex, overrides block base fee

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "tenderly_simulateBundle",
  "params": [
    [
      {
        "from": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
        "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "data": "0x095ea7b300000000000000000000000020a5814b73ef3537c6e099a0d45c798f4bd6e1d60000000000000000000000000000000000000000000000000000000000000001"
      },
      {
        "from": "0x20a5814b73ef3537c6e099a0d45c798f4bd6e1d6",
        "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "data": "0x23b872dd000000000000000000000000d8da6bf26964af9d7eed9e03e53415d37aa9604500000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001"
      }
    ],
    "0xF4D880"
  ]
}
```
{% endtab %}

{% tab title="cURL" %}
<pre class="language-bash"><code class="lang-bash">
<strong>curl https://mainnet.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
</strong>-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "tenderly_simulateBundle",
  "params": [
    [
      {
        "from": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
        "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "data": "0x095ea7b300000000000000000000000020a5814b73ef3537c6e099a0d45c798f4bd6e1d60000000000000000000000000000000000000000000000000000000000000001"
      },
      {
        "from": "0x20a5814b73ef3537c6e099a0d45c798f4bd6e1d6",
        "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "data": "0x23b872dd000000000000000000000000d8da6bf26964af9d7eed9e03e53415d37aa9604500000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001"
      }
    ],
    "0xF4D880"
  ]
}'

</code></pre>
{% endtab %}

{% tab title="ethers" %}
```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runSimulateTransaction() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.send("tenderly_simulateBundle", [
    [
      {
        "from": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
        "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "data": "0x095ea7b300000000000000000000000020a5814b73ef3537c6e099a0d45c798f4bd6e1d60000000000000000000000000000000000000000000000000000000000000001"
      },
      {
        "from": "0x20a5814b73ef3537c6e099a0d45c798f4bd6e1d6",
        "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "data": "0x23b872dd000000000000000000000000d8da6bf26964af9d7eed9e03e53415d37aa9604500000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001"
      }
    ],
    "0xF4D880",
  ]);

  // Print the output to console
  console.log(result);
}

(async () => {
  runSimulateTransaction();
})();
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": [
    {
      "status": true,
      "gasUsed": "0xb3a8",
      "cumulativeGasUsed": "0x0",
      "blockNumber": "0xf4d881",
      "type": "0x0",
      "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000800000000000000000000002000000080000000000000000200000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000000000000000000000000000000000004000000000000000000000000080000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000010200000800000000000000000000000000000000000000000000000000000",
      "logs": [
        {
          "name": "Approval",
          "anonymous": false,
          "inputs": [
            {
              "value": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
              "type": "address",
              "name": "src"
            },
            {
              "value": "0x20a5814b73ef3537c6e099a0d45c798f4bd6e1d6",
              "type": "address",
              "name": "guy"
            },
            {
              "value": "1",
              "type": "uint256",
              "name": "wad"
            }
          ],
          "raw": {
            "address": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
            "topics": [
              "0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925",
              "0x000000000000000000000000d8da6bf26964af9d7eed9e03e53415d37aa96045",
              "0x00000000000000000000000020a5814b73ef3537c6e099a0d45c798f4bd6e1d6"
            ],
            "data": "0x0000000000000000000000000000000000000000000000000000000000000001"
          }
        }
      ],
      "trace": [
        {
          "type": "CALL",
          "from": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
          "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
          "gas": "0x5f58cbc",
          "gasUsed": "0x5f64",
          "value": "0x0",
          "input": "0x095ea7b300000000000000000000000020a5814b73ef3537c6e099a0d45c798f4bd6e1d60000000000000000000000000000000000000000000000000000000000000001",
          "decodedInput": [
            {
              "value": "0x20a5814b73ef3537c6e099a0d45c798f4bd6e1d6",
              "type": "address",
              "name": "guy"
            },
            {
              "value": "1",
              "type": "uint256",
              "name": "wad"
            }
          ],
          "method": "approve",
          "output": "0x0000000000000000000000000000000000000000000000000000000000000001",
          "decodedOutput": [
            {
              "value": true,
              "type": "bool",
              "name": ""
            }
          ],
          "subtraces": 0,
          "traceAddress": [
            0
          ]
        }
      ]
    },
    {
      "status": true,
      "gasUsed": "0x8a78",
      "cumulativeGasUsed": "0x0",
      "blockNumber": "0xf4d881",
      "type": "0x0",
      "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002000000080000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000020000000000000000000800000000000000000000000010000000000000004000000000000000000000000080000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000020000000200000800000000000000000000000000000000000000000000000000000",
      "logs": [
        {
          "name": "Transfer",
          "anonymous": false,
          "inputs": [
            {
              "value": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
              "type": "address",
              "name": "src"
            },
            {
              "value": "0x0000000000000000000000000000000000000000",
              "type": "address",
              "name": "dst"
            },
            {
              "value": "1",
              "type": "uint256",
              "name": "wad"
            }
          ],
          "raw": {
            "address": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
            "topics": [
              "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
              "0x000000000000000000000000d8da6bf26964af9d7eed9e03e53415d37aa96045",
              "0x0000000000000000000000000000000000000000000000000000000000000000"
            ],
            "data": "0x0000000000000000000000000000000000000000000000000000000000000001"
          }
        }
      ],
      "trace": [
        {
          "type": "CALL",
          "from": "0x20a5814b73ef3537c6e099a0d45c798f4bd6e1d6",
          "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
          "gas": "0x5f58c3c",
          "gasUsed": "0x4874",
          "value": "0x0",
          "input": "0x23b872dd000000000000000000000000d8da6bf26964af9d7eed9e03e53415d37aa9604500000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001",
          "decodedInput": [
            {
              "value": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
              "type": "address",
              "name": "src"
            },
            {
              "value": "0x0000000000000000000000000000000000000000",
              "type": "address",
              "name": "dst"
            },
            {
              "value": "1",
              "type": "uint256",
              "name": "wad"
            }
          ],
          "method": "transferFrom",
          "output": "0x0000000000000000000000000000000000000000000000000000000000000001",
          "decodedOutput": [
            {
              "value": true,
              "type": "bool",
              "name": ""
            }
          ],
          "subtraces": 0,
          "traceAddress": [
            0
          ]
        }
      ]
    }
  ]
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Simulations result `ARRAY`: list of simulation results in a bundle

* **status** `NUMBER:` either `1` (success) or `0` (failure)
* **gasUsed** `NUMBER`: The amount of gas used by this specific transaction alone
* **cumulativeGasUsed** `NUMBER`: the total amount of gas used when this transaction was executed in the block
* **blockNumber** `NUMBER`: the block number in which this transaction was simulated
* **type** `NUMBER`: transaction type, `0x00` for legacy transactions, `0x01` for access list types, `0x02` for dynamic fees
* **logsBloom** `STRING`: bloom filter for light clients to quickly retrieve related logs
* **logs**: an array of emitted events `ARRAY` of `OBJECT`
  * **name** `STRING`: event name
  * **anonymous** `BOOLEAN`: indicates if event is anonymous
  * **inputs**: array of decoded log arguments `ARRAY` of decoded logs `OBJECT`
    * **name** `STRING`: event argument name
    * **type** `STRING`: event argument type from Solidity type system
    * **value** (_optional_) `STRING` string representation value of the argument; interpret according to the `type` field
  * **raw** `OBJECT`: raw logs
    * **address** `STRING` hex encoded address: address of the contract emitting the log
    * **topics** `ARRAY` of `STRING` 32 hex encoded bytes
    * **data** `STRING` hex encoded string representing event data
* **trace**: Trace `ARRAY` of `OBJECT`
  * **type** `STRING` type: trace item type - either `CALL`| `CALLCODE`| `STATICCALL`| `DELEGATECALL`| `CREATE`| `CREATE2`| `SELFDESTRUCT`
  * **from** `STRING`: hex encoded address
  * **to** `STRING`: hex encoded address
  * **gas** `STRING`: hex encoded unsigned 64 byte integer representing event gas
  * **gasUsed** `STRING`: hex encoded unsigned 64 byte integer representing event gasUsed
  * **value** `STRING`: hex encoded unsigned 64 byte integer representing event value in wei
  * **error** `STRING`: low-level error from virtual machine
  * **errorReason** `STRING`: extracted error reason in case of revert
  * **input** `STRING`: hex encoded string representation of raw input bytes for the trace point
  * **method** `STRING`: invoked contract method
  * **decodedInput** : decoded input for the invoked method - `ARRAY` of decoded in argument `OBJECT`
    * **value** `STRING`: string representation value of the argument; interpret according to the `type` field.
    * **type** `STRING`: the Solidity type of this argument
    * **name** `STRING`: the name of this argument
  * **output** `STRING`: raw trace output
  * **decodedOutput** : decoded output of the invoked method - `ARRAY` of decoded out argument `OBJECT`
    * **value** `STRING`: string representation value of the argument; interpret according to the `type` field.
    * **type** `STRING`: the Solidity type of this argument
    * **name** `STRING`: the name of this argument
  * **subtraces** `NUMBER`: number of child traces
  * **traceAddress** : trace position `ARRAY` of `NUMBER`
