---
description: A detailed overview of supported Ethereum JSON RPC calls.
---

# Detailed JSON RPC reference

{% hint style="info" %}
This page shows detailed overview of supported Ethereum JSON RPC calls. Find a [brief list of supported calls](brief-json-rpc.md).
{% endhint %}

### `eth_getBlockByHash`

Returns information about a block by hash.

[Brief version](brief-json-rpc.md#eth\_getBlockByHash)

**PARAMS**

1. **Block hash**The hash of the block `STRING` 32 byte hex value
2. **Hydrated transactions** `BOOLEAN` hydrated

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getBlockByHash", [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    false,
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "number": "0x77ed36",
    "hash": "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    "parentHash": "0xdf9734476dcc360d864e31cc8422ce96f8aa8dff9a827b57f2c3c4ec8f71c421",
    "nonce": "0x0000000000000000",
    "mixHash": "0x3dd2d65fcd45d469cdca6e524382053d27b9e36b2b2e2f5808247c406d6bafd5",
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "logsBloom": "0x00300000000000080000000800800800000040c000080012000888102002041000000000020002000020000040000800000008000002404100001000402468300844000080000008880800280808090000000001001400000000290040000800000400004200088001402280800008120d000040104000000000001000800080000000840060480001020000000005000000008028000204010208008020004002050800500002900000083080000000010000010400006100100000000000200804900200000800051400001800a050000008240001001000000028008060201034004000020011200008080000008880080008000048019040000081000010",
    "stateRoot": "0x1a6a2f5902392bf771ec405d427eae2df1c634ed26705e182e48adb893e2fa22",
    "miner": "0x4d496ccc28058b1d74b7a19541663e21154f9c84",
    "difficulty": "0x0",
    "extraData": "0x",
    "size": "0xead",
    "gasLimit": "0x1c9c380",
    "gasUsed": "0x20af8f",
    "timestamp": "0x635e2a44",
    "transactionsRoot": "0x24254b70d82f362e21f82ca841a893d1fe714fcdadba260fac0032359a40d9d8",
    "receiptsRoot": "0x956eb9e1ec572a6d044663dc0085bf421d6cf49193e383b4dc004c36e2f676e5",
    "baseFeePerGas": "0x10",
    "totalDifficulty": "0xa4a470",
    "uncles": [],
    "transactions": [
      "0xea5bbd6f391894557eec975d161391f25ce4cf86cc404964a2c39957b11dad43",
      "0x08f23a8d29dc0b23989b648f11fd89fad609c6694305b5d35e9b6d5fe1616d3a",
      "0x912b1146c5bc2c17b2e0726cc43d51ba9d22e19cd0a38dd248062520349db02b",
      "0xf10ba2f27477339095f9e7b60611812d6ca2a75e69e72f6acb64e2b109ae74b8",
      "0x559fd3851c1470cac199885335676fedcdde9789aee0ad894feef6705be7139c",
      "0x2ecf200a6c4da6478430acfac77a58fe90bd9c7db8c5bc19059eecd87dbb6794",
      "0xe5227c1cc37b2c7af8ef050fbc56913425b01b82b1866fa5099ba512630ae7d1",
      "0x4033bed32cca181377b703e742f092142447a0ab65ae4c1fb8a156d816ac397f",
      "0x6d8d45835f7101188cb9e7b5e8fb18e3d1fdc3bd26e3417ffbed63423a936c37",
      "0xe78704b2a82a49603ca2cdeffde7543911b68207ff397ed756e19da125e3eda6"
    ]
  }
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Block information Block object `OBJECT`

* **parentHash** `STRING` Parent block hash
* **sha3Uncles** `STRING` Ommers hash
* **miner** `STRING` Coinbase
* **stateRoot** `STRING` State root
* **transactionsRoot** `STRING` Transactions root
* **receiptsRoot** `STRING` Receipts root
* **logsBloom** `STRING` Bloom filter
* **difficulty** (_optional_) `STRING` Difficulty
* **number** `STRING` Number
* **gasLimit** `STRING` Gas limit
* **gasUsed** `STRING` Gas used
* **timestamp** `STRING` Timestamp
* **extraData** `STRING` Extra data
* **mixHash** `STRING` Mix hash
* **nonce** `STRING` Nonce
* **totalDifficulty** (_optional_) `STRING` Total difficult
* **baseFeePerGas** (_optional_) `STRING` Base fee per gas
* **size** `STRING` Block size
* **transactions** `ANYOF` of
  * Transaction hashes `ARRAY` of `STRING` 32 byte hex value
  * Full transactions `ARRAY` of
    * Signed 1559 Transaction `OBJECT`
      * **type** `STRING` type
      * **nonce** `STRING` nonce
      * **to** (_optional_) `STRING` to address
      * **gas** `STRING` gas limit
      * **value** `STRING` value
      * **input** `STRING` input data
      * **maxPriorityFeePerGas** `STRING` max priority fee per gas: Maximum fee per gas the sender is willing to pay to miners in wei
      * **maxFeePerGas** `STRING` max fee per gas: The maximum total fee per gas the sender is willing to pay (includes the network / base fee and miner / priority fee) in wei
      * **accessList** accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
        * **address** (_optional_) `STRING` hex encoded address
        * **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
      * **chainId** `STRING` chainId: Chain ID that this transaction is valid on.
      * **yParity** `STRING` yParity: The parity (0 for even, 1 for odd) of the y-value of the secp256k1 signature.
      * **r** `STRING` r
      * **s** `STRING` s
    * Signed 2930 Transaction `OBJECT`
      * **type** `STRING` type
      * **nonce** `STRING` nonce
      * **to** (_optional_) `STRING` to address
      * **gas** `STRING` gas limit
      * **value** `STRING` value
      * **input** `STRING` input data
      * **gasPrice** `STRING` gas price: The gas price willing to be paid by the sender in wei
      * **accessList** accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
        * **address** (_optional_) `STRING` hex encoded address
        * **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
      * **chainId** `STRING` chainId: Chain ID that this transaction is valid on.
      * **yParity** `STRING` yParity: The parity (0 for even, 1 for odd) of the y-value of the secp256k1 signature.
      * **r** `STRING` r
      * **s** `STRING` s
    * Signed Legacy Transaction `OBJECT`
      * **type** `STRING` type
      * **nonce** `STRING` nonce
      * **to** (_optional_) `STRING` to address
      * **gas** `STRING` gas limit
      * **value** `STRING` value
      * **input** `STRING` input data
      * **gasPrice** `STRING` gas price: The gas price willing to be paid by the sender in wei
      * **chainId** (_optional_) `STRING` chainId: Chain ID that this transaction is valid on.
      * **v** `STRING` v
      * **r** `STRING` r
      * **s** `STRING` s
* **uncles** Uncles `ARRAY` of `STRING` 32 byte hex value

### `eth_getBlockByNumber`

Returns information about a block by number.

[Brief version](brief-json-rpc.md#eth\_getBlockByNumber)

**PARAMS**

1\. **Block**

* `STRING` Block number
* `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

2\. **Hydrated transactions** `BOOLEAN` hydrated

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getBlockByNumber", ["latest", false]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "number": "0x7aa3a9",
    "hash": "0xd65ea6ed7a1204d48c3f172aa052efabf1e3ebfbab251e5ffb55e2cac8b511d5",
    "parentHash": "0x988e81a9643753ac9959780087370985cc2070ed67c52d5949e7389ff3b43c76",
    "nonce": "0x0000000000000000",
    "mixHash": "0x1cc7290c64fbeaa6a2390a992b304e6b0e89d738acbda2eba58eb65429f74a0f",
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "logsBloom": "0x00a001092200000e04021201860000002808a00000010002001100000000040040002008200000690000040a04048450004140144200000c04006a01202482c01000024004288850c084800800010122000014000296004000510c0080004140000000000a0200404201000008440800004000088880620420102010028002040000002008040318cc400004000000001000001122480888000000600b4000000202804c44020020040404c0240120000842b480002081404023004010880650401450420000000840001e0100200410002000201010801002c04000028060400910001008100c400112000208c8003020100000020012510000401008000880",
    "stateRoot": "0x2e3c31aa466540e4c9ca562f562b7e1b4edff1f6453f5b15071f308e095a1791",
    "miner": "0xf36f155486299ecaff2d4f5160ed5114c1f66000",
    "difficulty": "0x0",
    "extraData": "0x",
    "size": "0x1f06",
    "gasLimit": "0x1c9c380",
    "gasUsed": "0x35f28e",
    "timestamp": "0x6384f504",
    "transactionsRoot": "0xb40ced8fd738c03d1101d4ed0aecb6b290c7c54230bafc92f3303240b056d957",
    "receiptsRoot": "0xcac0a3181c307c3b77e076fa557a06e97659f7fef07993935a16dd301021efcb",
    "baseFeePerGas": "0x1ce43b283",
    "totalDifficulty": "0xa4a470",
    "uncles": [],
    "transactions": [
      "0x5b0696572afb2c544efebf62d7e0eea2520b2cd74156ced8dbe3294d44209b25",
      "0x052242bf239f5fc8b5bb2f156cf22ef6ce2eb738304ba3a7d5998c15d2a97140",
      "0x3efdf4bc4f2b3c0ffbbd1508dbe6e198315f4a239e8d5e55713f9feb1eadeb49",
      "0xd4cc079012c245c55ec929f7bad97aefcbafdbb9df3b66a76e812714887c607c",
      "0xc7b29089a46aefbb6de2fdd65cf3d8914bd104e093ba0c2edfa410649665cc6c",
      "0x20a573986ec0a56d01292e23b24788ca8438883e32a04cf1cc44a6244a35f562",
      "0x160daaf007c66dacc2849a3a2a4c212f223762a780c0bc3c3e95e4d152a62ef9",
      "0x7e520c067a8943ef14cb867b882fb2e7a22b3015c9b4c9998a97a03d6003bed4",
      "0x50a2c03cb33be9a371f8814f1557cb6d4569b4e2bec308156109268dd803e212",
      "0xdd731274cbeb96d9c754bc2a191fd59b51811ad0d432c060d8c5676c0ea67fa9",
      "0x4e32fdef7b398ec1f83e7d4a23a2b31274c69e0018bae1cb619cac8dd7adb450",
      "0x5ef6c92d1e34d40eb0b0ccbf7f8ae1a6b46aa65093632a40f76c1dcbe0cff8ed",
      "0xacee7050d37de355b942dc661337c06ef0e2fe13cf7bbca1ea37753cffdd1c90",
      "0x82247b876b0a25b281d4e752af62f6c54478995bd785914a5573565fd76fe8e8",
      "0xbc93b221f37b785848dedd47f63ec1f64ccb2f5182c29a2f3033d3c8dab4156b",
      "0xfc328bcef60eccae79f9e2f8666ec5b29774435f940dd89870a449c0466e2f62",
      "0x658be3de19f2cf3bb8849e4ef2008b71c47493b167d4d0874ab25d6af3f62b53",
      "0xbb7d18283c0d34d3d6f9ed359a7a9f7d8980c7b5a69118bd5d6cad9e8a810a9f"
    ]
  }
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Block information Block object `OBJECT`

* **parentHash** `STRING` Parent block hash
* **sha3Uncles** `STRING` Ommers hash
* **miner** `STRING` Coinbase
* **stateRoot** `STRING` State root
* **transactionsRoot** `STRING` Transactions root
* **receiptsRoot** `STRING` Receipts root
* **logsBloom** `STRING` Bloom filter
* **difficulty** (_optional_) `STRING` Difficulty
* **number** `STRING` Number
* **gasLimit** `STRING` Gas limit
* **gasUsed** `STRING` Gas used
* **timestamp** `STRING` Timestamp
* **extraData** `STRING` Extra data
* **mixHash** `STRING` Mix hash
* **nonce** `STRING` Nonce
* **totalDifficulty** (_optional_) `STRING` Total difficult
* **baseFeePerGas** (_optional_) `STRING` Base fee per gas
* **size** `STRING` Block size
* **transactions** `ANYOF` of
  * Transaction hashes `ARRAY` of `STRING` 32 byte hex value
  * Full transactions `ARRAY` of
    * Signed 1559 Transaction `OBJECT`
      * **type** `STRING` type
      * **nonce** `STRING` nonce
      * **to** (_optional_) `STRING` to address
      * **gas** `STRING` gas limit
      * **value** `STRING` value
      * **input** `STRING` input data
      * **maxPriorityFeePerGas** `STRING` max priority fee per gas: Maximum fee per gas the sender is willing to pay to miners in wei
      * **maxFeePerGas** `STRING` max fee per gas: The maximum total fee per gas the sender is willing to pay (includes the network / base fee and miner / priority fee) in wei
      * **accessList** accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
        * **address** (_optional_) `STRING` hex encoded address
        * **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
      * **chainId** `STRING` chainId: Chain ID that this transaction is valid on.
      * **yParity** `STRING` yParity: The parity (0 for even, 1 for odd) of the y-value of the secp256k1 signature.
      * **r** `STRING` r
      * **s** `STRING` s
    * Signed 2930 Transaction `OBJECT`
      * **type** `STRING` type
      * **nonce** `STRING` nonce
      * **to** (_optional_) `STRING` to address
      * **gas** `STRING` gas limit
      * **value** `STRING` value
      * **input** `STRING` input data
      * **gasPrice** `STRING` gas price: The gas price willing to be paid by the sender in wei
      * **accessList** accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
        * **address** (_optional_) `STRING` hex encoded address
        * **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
      * **chainId** `STRING` chainId: Chain ID that this transaction is valid on.
      * **yParity** `STRING` yParity: The parity (0 for even, 1 for odd) of the y-value of the secp256k1 signature.
      * **r** `STRING` r
      * **s** `STRING` s
    * Signed Legacy Transaction `OBJECT`
      * **type** `STRING` type
      * **nonce** `STRING` nonce
      * **to** (_optional_) `STRING` to address
      * **gas** `STRING` gas limit
      * **value** `STRING` value
      * **input** `STRING` input data
      * **gasPrice** `STRING` gas price: The gas price willing to be paid by the sender in wei
      * **chainId** (_optional_) `STRING` chainId: Chain ID that this transaction is valid on.
      * **v** `STRING` v
      * **r** `STRING` r
      * **s** `STRING` s
* **uncles** Uncles `ARRAY` of `STRING` 32 byte hex value

### `eth_getBlockTransactionCountByHash`

Returns the number of transactions in a block from a block matching the given block hash.

[Brief version](brief-json-rpc.md#eth\_getBlockTransactionCountByHash)

**PARAMS**

1. **Block hash** (_optional_) `STRING` 32 byte hex value

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getBlockTransactionCountByHash", [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0xa"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Transaction count `STRING` hex encoded unsigned integer

### `eth_getBlockTransactionCountByNumber`

Returns the number of transactions in a block matching the given block number.

[Brief version](brief-json-rpc.md#eth\_getBlockTransactionCountByNumber)

**PARAMS**

1. **Block** (_optional_)

* `STRING` Block number
* `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getBlockTransactionCountByNumber", [
    "latest",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x12"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Transaction count `STRING` hex encoded unsigned integer

### `eth_getUncleCountByBlockHash`

Returns the number of uncles in a block from a block matching the given block hash.

[Brief version](brief-json-rpc.md#eth\_getUncleCountByBlockHash)

**PARAMS**

1. **Block hash** (_optional_) `STRING` 32 byte hex value

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getUncleCountByBlockHash", [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x0"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Uncle count `STRING` hex encoded unsigned integer

### `eth_getUncleCountByBlockNumber`

Returns the number of transactions in a block matching the given block number.

[Brief version](brief-json-rpc.md#eth\_getUncleCountByBlockNumber)

**PARAMS**

1. **Block** (_optional_)

* `STRING` Block number
* `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getUncleCountByBlockNumber", [
    "latest",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x0"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Uncle count `STRING` hex encoded unsigned integer

### `eth_chainId`

Returns the chain ID of the current network.

[Brief version](brief-json-rpc.md#eth\_chainId)

**PARAMS**

none

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_chainId", []);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x5"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Chain ID `STRING` hex encoded unsigned integer

### `eth_syncing`

Returns an object with data about the sync status or false.

[Brief version](brief-json-rpc.md#eth\_syncing)

**PARAMS**

none

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_syncing", []);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": false
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Syncing status `ONEOF`

* Syncing progress `OBJECT`
  * **startingBlock** (_optional_) `STRING` Starting block
  * **currentBlock** (_optional_) `STRING` Current block
  * **highestBlock** (_optional_) `STRING` Highest block
* `BOOLEAN` Not syncing

### `eth_accounts`

Returns a list of addresses owned by client.

[Brief version](brief-json-rpc.md#eth\_accounts)

**PARAMS**

none

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_accounts", []);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": []
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Accounts `ARRAY` of `STRING` hex encoded address

### `eth_blockNumber`

Returns the number of most recent block.

[Brief version](brief-json-rpc.md#eth\_blockNumber)

**PARAMS**

none

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_blockNumber", []);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x7aa3a9"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Block number `STRING` hex encoded unsigned integer

### `eth_call`

Executes a new message call immediately without creating a transaction on the block chain.

[Brief version](brief-json-rpc.md#eth\_call)

**PARAMS**

1. **Transaction** Transaction object generic to all types `OBJECT`
   * **type** (_optional_) `STRING` type
   * **nonce** (_optional_) `STRING` nonce
   * **to** (_optional_) `STRING` to address
   * **from** (_optional_) `STRING` from address
   * **gas** (_optional_) `STRING` gas limit
   * **value** (_optional_) `STRING` value
   * **input** (_optional_) `STRING` input data
   * **gasPrice** (_optional_) `STRING` gas price: The gas price willing to be paid by the sender in wei
   * **maxPriorityFeePerGas** (_optional_) `STRING` max priority fee per gas: Maximum fee per gas the sender is willing to pay to miners in wei
   * **maxFeePerGas** (_optional_) `STRING` max fee per gas: The maximum total fee per gas the sender is willing to pay (includes the network / base fee and miner / priority fee) in wei
   * **accessList** (_optional_) accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
   * **address** (_optional_) `STRING` hex encoded address
   * **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
   * **chainId** (_optional_) `STRING` chainId: Chain ID that this transaction is valid on.
2. &#x20;**Block** (_optional_)
   * `STRING` Block number
   * `ENUM` of Block tag `earliest|finalized|safe|latest|pending`
3. &#x20;**State Overrides** (_optional_) `MAP`: mapping from an account (address) to override specification
   * **key** `STRING`: the account this override applies to
   * **value** `OBJECT`: the override specification
     * **nonce** (_optional_) `STRING`: hex encoded 8 byte nonce override for the account
     * **code** (_optional_) `STRING`: data of the code override for the account
     * **balance** (_optional_) `STRING`: hex encoded 32 byte balance override for the account in wei
     * **stateDiff** (_optional_) `MAP`: mapping of storage key to storage value override
       * **key** `STRING`: the storage key
       * **value** `STRING`: the value override for the given storage key
4. **Block Overrides** (optional) `OBJECT`: The set of header fields to override in a block.&#x20;
   * **number** _(optional)_ `STRING`: hex, overrides the block number
   * **difficulty** _(optional)_ `STRING`: hex, overrides the block difficulty
   * **time** (_optional_) `STRING`: hex, overrides block timestamp
   * **gasLimit** _(optional)_ `STRING`: hex, overrides block timestamp
   * **coinbase** _(optional)_ `STRING`: hex, overrides block miner
   * **random** _(optional)_ `STRING`: hex, overrides the blocks extra data which feeds into the RANDOM opcode
   * **baseFee** _(optional)_ `STRING`: hex, overrides block base fee

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_call",
  "params": [
    {
      "from": "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
      "to": "0xff39a3e734fe363e631441f6d24c7539240c2628",
      "value": "0x0",
      "data": "0x2e7700f0"
    },
    "latest"
  ]
}
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_call",
  "params": [
    {
      "from": "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
      "to": "0xff39a3e734fe363e631441f6d24c7539240c2628",
      "value": "0x0",
      "data": "0x2e7700f0"
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
  const result = await provider.send("eth_call", [
    {
      from: "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
      to: "0xff39a3e734fe363e631441f6d24c7539240c2628",
      value: "0x0",
      data: "0x2e7700f0",
    },
    "latest",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x0000000000000000000000000000000000000000000000000000000000000001"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Return data `STRING` hex encoded bytes

### `eth_estimateGas`

Generates and returns an estimate of how much gas is necessary to allow the transaction to complete.

[Brief version](brief-json-rpc.md#eth\_estimateGas)

**PARAMS**

1. **Transaction** Transaction object generic to all types `OBJECT`
   * **type** (_optional_) `STRING` type
   * **nonce** (_optional_) `STRING` nonce
   * **to** (_optional_) `STRING` to address
   * **from** (_optional_) `STRING` from address
   * **gas** (_optional_) `STRING` gas limit
   * **value** (_optional_) `STRING` value
   * **input** (_optional_) `STRING` input data
   * **gasPrice** (_optional_) `STRING` gas price: The gas price willing to be paid by the sender in wei
   * **maxPriorityFeePerGas** (_optional_) `STRING` max priority fee per gas: Maximum fee per gas the sender is willing to pay to miners in wei
   * **maxFeePerGas** (_optional_) `STRING` max fee per gas: The maximum total fee per gas the sender is willing to pay (includes the network / base fee and miner / priority fee) in wei
   * **accessList** (_optional_) accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
   * **address** (_optional_) `STRING` hex encoded address
   * **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
   * **chainId** (_optional_) `STRING` chainId: Chain ID that this transaction is valid on.
2. &#x20;**Block** (_optional_)
   * `STRING` Block number
   * `ENUM` of Block tag `earliest|finalized|safe|latest|pending`
3. &#x20;**State Overrides** (_optional_) `MAP`: mapping from an account (address) to override specification
   * **key** `STRING`: the account this override applies to
   * **value** `OBJECT`: the override specification
     * **nonce** (_optional_) `STRING`: hex encoded 8 byte nonce override for the account
     * **code** (_optional_) `STRING`: data of the code override for the account
     * **balance** (_optional_) `STRING`: hex encoded 32 byte balance override for the account in wei
     * **stateDiff** (_optional_) `MAP`: mapping of storage key to storage value override
       * **key** `STRING`: the storage key
       * **value** `STRING`: the value override for the given storage key
4. **Block Overrides** (optional) `OBJECT`: The set of header fields to override in a block.&#x20;
   * **number** _(optional)_ `STRING`: hex, overrides the block number
   * **difficulty** _(optional)_ `STRING`: hex, overrides the block difficulty
   * **time** (_optional_) `STRING`: hex, overrides block timestamp
   * **gasLimit** _(optional)_ `STRING`: hex, overrides block timestamp
   * **coinbase** _(optional)_ `STRING`: hex, overrides block miner
   * **random** _(optional)_ `STRING`: hex, overrides the blocks extra data which feeds into the RANDOM opcode
   * **baseFee** _(optional)_ `STRING`: hex, overrides block base fee

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_estimateGas",
  "params": [
    {
      "from": "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
      "to": "0xff39a3e734fe363e631441f6d24c7539240c2628",
      "value": "0x0",
      "data": "0x2e7700f0"
    },
    "latest"
  ]
}
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_estimateGas",
  "params": [
    {
      "from": "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
      "to": "0xff39a3e734fe363e631441f6d24c7539240c2628",
      "value": "0x0",
      "data": "0x2e7700f0"
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
  const result = await provider.send("eth_estimateGas", [
    {
      from: "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
      to: "0xff39a3e734fe363e631441f6d24c7539240c2628",
      value: "0x0",
      data: "0x2e7700f0",
    },
    "latest",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x5bf6"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Gas used `STRING` hex encoded unsigned integer

### `eth_createAccessList`

Generates an access list for a transaction.

[Brief version](brief-json-rpc.md#eth\_createAccessList)

**PARAMS**

1. **Transaction** Transaction object generic to all types `OBJECT`

* **type** (_optional_) `STRING` type
* **nonce** (_optional_) `STRING` nonce
* **to** (_optional_) `STRING` to address
* **from** (_optional_) `STRING` from address
* **gas** (_optional_) `STRING` gas limit
* **value** (_optional_) `STRING` value
* **input** (_optional_) `STRING` input data
* **gasPrice** (_optional_) `STRING` gas price: The gas price willing to be paid by the sender in wei
* **maxPriorityFeePerGas** (_optional_) `STRING` max priority fee per gas: Maximum fee per gas the sender is willing to pay to miners in wei
* **maxFeePerGas** (_optional_) `STRING` max fee per gas: The maximum total fee per gas the sender is willing to pay (includes the network / base fee and miner / priority fee) in wei
* **accessList** (_optional_) accessList: EIP-2930 access list `ARRAY` of Access list entry `OBJECT`
  * **address** (_optional_) `STRING` hex encoded address
  * **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
* **chainId** (_optional_) `STRING` chainId: Chain ID that this transaction is valid on.

1. **Block** (_optional_)

* `STRING` Block number
* `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_createAccessList",
  "params": [
    {
      "from": "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
      "to": "0xff39a3e734fe363e631441f6d24c7539240c2628",
      "value": "0x0",
      "data": "0x2e7700f0"
    },
    "latest"
  ]
}
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_createAccessList",
  "params": [
    {
      "from": "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
      "to": "0xff39a3e734fe363e631441f6d24c7539240c2628",
      "value": "0x0",
      "data": "0x2e7700f0"
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

async function runCreateAccessList() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.send("eth_createAccessList", [
    {
      from: "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
      to: "0xff39a3e734fe363e631441f6d24c7539240c2628",
      value: "0x0",
      data: "0x2e7700f0",
    },
    "latest",
  ]);

  // Print the output to console
  console.log(result);
}

(async () => {
  runCreateAccessList();
})();
```
{% endtab %}

{% tab title="Response" %}
```json
N/A
```
{% endtab %}
{% endtabs %}

**RESULT**: Gas used Access list result `OBJECT`

* **accessList** (_optional_) accessList `ARRAY` of Access list entry `OBJECT`
  * **address** (_optional_) `STRING` hex encoded address
  * **storageKeys** (_optional_) `ARRAY` of `STRING` 32 byte hex value
* **error** (_optional_) `STRING` error
* **gasUsed** (_optional_) `STRING` Gas used

### `eth_gasPrice`

Returns the current price per gas in wei.

[Brief version](brief-json-rpc.md#eth\_gasPrice)

**PARAMS**

none

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_gasPrice", []);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x1d4399383"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Gas price `STRING` Gas price

### `eth_maxPriorityFeePerGas`

Returns the current maxPriorityFeePerGas per gas in wei.

[Brief version](brief-json-rpc.md#eth\_maxPriorityFeePerGas)

**PARAMS**

none

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_maxPriorityFeePerGas", []);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x5f5e100"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Max priority fee per gas `STRING` Max priority fee per gas

### `eth_feeHistory`

Transaction fee history

[Brief version](brief-json-rpc.md#eth\_feeHistory)

**PARAMS**

1. **blockCount**Requested range of blocks. Clients will return less than the requested range if not all blocks are available. `STRING` hex encoded unsigned integer
2. **newestBlock**Highest block of the requested range.

* `STRING` Block number
* `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

1. **rewardPercentiles**A monotonically increasing list of percentile values. For each block in the requested range, the transactions will be sorted in ascending order by effective tip per gas and the coresponding effective tip for the percentile will be determined, accounting for gas consumed. `ARRAY` of `NUMBER`NaN

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_feeHistory", [2, "latest", []]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "oldestBlock": "0x7aa3a8",
    "baseFeePerGas": ["0x1ad6095b4", "0x1ce43b283", "0x1a219d20a"],
    "gasUsedRatio": [0.8063707333333333, 0.11785006666666667]
  }
}
```
{% endtab %}
{% endtabs %}

**RESULT**: feeHistoryResult Fee history for the returned block range. This can be a subsection of the requested range if not all blocks are available.feeHistoryResults `OBJECT`

* **oldestBlock** `STRING` oldestBlock: Lowest number block of returned range.
* **baseFeePerGas** baseFeePerGasArray: An array of block base fees per gas. This includes the next block after the newest of the returned range, because this value can be derived from the newest block. Zeroes are returned for pre-EIP-1559 blocks. `ARRAY` of `STRING` hex encoded unsigned integer
* **reward** (_optional_) rewardArray: A two-dimensional array of effective priority fees per gas at the requested block percentiles. `ARRAY` of `ARRAY` of `STRING` rewardPercentile

### `eth_newFilter`

Creates a filter object, based on filter options, to notify when the state changes (logs).

[Brief version](brief-json-rpc.md#eth\_newFilter)

**PARAMS**

1. **Filter** (_optional_) filter `OBJECT`

* **fromBlock** (_optional_) `STRING` from block
* **toBlock** (_optional_) `STRING` to block
* **address** (_optional_) `ONEOF` of Address(es)
  * `STRING` Address
  * `ARRAY` of `STRING` hex encoded address
*   **topics** (_optional_) Topics `ARRAY` of - `NULL`

    ```
    - `STRING` Single Topic Match

    - `ARRAY` of `STRING` 32 hex encoded bytes
    ```

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_newFilter",
  "params": [
    {
      "fromBlock": 7878500,
      "toBlock": 7878700,
      "topics": [
        "0x5445f318f4f5fcfb66592e68e0cc5822aa15664039bd5f0ffde24c5a8142b1ac",
        "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
        "0x0000000000000000000000000000000000000000000000000000000000000000"
      ]
    }
  ]
}
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_newFilter",
  "params": [
    {
      "fromBlock": 7878500,
      "toBlock": 7878700,
      "topics": [
        "0x5445f318f4f5fcfb66592e68e0cc5822aa15664039bd5f0ffde24c5a8142b1ac",
        "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
        "0x0000000000000000000000000000000000000000000000000000000000000000"
      ]
    }
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
  const result = await provider.send("eth_newFilter", [
    {
      fromBlock: 7878500,
      toBlock: 7878700,
      topics: [
        "0x5445f318f4f5fcfb66592e68e0cc5822aa15664039bd5f0ffde24c5a8142b1ac",
        "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
        "0x0000000000000000000000000000000000000000000000000000000000000000",
      ],
    },
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x2465bdd9b450df536ee0354ec06842aff8a09a8a3926d6d48e9980ed12115c39"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Filter Identifier `STRING` hex encoded unsigned integer

### `eth_newBlockFilter`

Creates a filter in the node, to notify when a new block arrives.

[Brief version](brief-json-rpc.md#eth\_newBlockFilter)

**PARAMS**

none

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_newBlockFilter", []);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0xdf045970f4888b186c85fb33bfb500736c615f49bb12211e7648801e01722dc0"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Filter Identifier `STRING` hex encoded unsigned integer

### `eth_newPendingTransactionFilter`

Creates a filter in the node, to notify when a new pending transaction arrives.

[Brief version](brief-json-rpc.md#eth\_newBlockFilter)

**PARAMS**

none

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_newPendingTransactionFilter",
  "params": []
}
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_newPendingTransactionFilter",
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
  const result = await provider.send("eth_newPendingTransactionFilter", []);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x5c085c6a8828b03e4ef82a5aaa710bb5bbcf0ccc04735f6a508c2d5210cdc2f9"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Filter Identifier `STRING` hex encoded unsigned integer

### `eth_getFilterChanges`

Polling method for a filter, which returns an array of logs which occurred since last poll.

[Brief version](brief-json-rpc.md#eth\_getFilterChanges)

**PARAMS**

1. **Filter Identifier** (_optional_) `STRING` hex encoded unsigned integer

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getFilterChanges",
  "params": [
    "0x433e8e72506124c82ccbb4095b73544422b46a5cc6b2557c386bddf1b0d1f736"
  ]
}
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getFilterChanges",
  "params": [
    "0x433e8e72506124c82ccbb4095b73544422b46a5cc6b2557c386bddf1b0d1f736"
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
  const result = await provider.send("eth_getFilterChanges", [
    "0x433e8e72506124c82ccbb4095b73544422b46a5cc6b2557c386bddf1b0d1f736",
  ]);

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

**RESULT**: Log objects `ONEOF`

* `ARRAY` of `STRING` 32 byte hex value
* `ARRAY` of `STRING` 32 byte hex value
* `ARRAY` of log `OBJECT`
  * **removed** (_optional_) `BOOLEAN` removed
  * **logIndex** (_optional_) `STRING` log index
  * **transactionIndex** (_optional_) `STRING` transaction index
  * **transactionHash** `STRING` transaction hash
  * **blockHash** (_optional_) `STRING` block hash
  * **blockNumber** (_optional_) `STRING` block number
  * **address** (_optional_) `STRING` address
  * **data** (_optional_) `STRING` data
  * **topics** (_optional_) topics `ARRAY` of `STRING` 32 hex encoded bytes

### `eth_getFilterLogs`

Returns an array of all logs matching filter with given id.

[Brief version](brief-json-rpc.md#eth\_getFilterLogs)

**PARAMS**

1. **Filter Identifier** (_optional_) `STRING` hex encoded unsigned integer

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getFilterLogs",
  "params": [
    "0x433e8e72506124c82ccbb4095b73544422b46a5cc6b2557c386bddf1b0d1f736"
  ]
}
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getFilterLogs",
  "params": [
    "0x433e8e72506124c82ccbb4095b73544422b46a5cc6b2557c386bddf1b0d1f736"
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
  const result = await provider.send("eth_getFilterLogs", [
    "0x433e8e72506124c82ccbb4095b73544422b46a5cc6b2557c386bddf1b0d1f736",
  ]);

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

**RESULT**: Log objects `ONEOF`

* `ARRAY` of `STRING` 32 byte hex value
* `ARRAY` of `STRING` 32 byte hex value
* `ARRAY` of log `OBJECT`
  * **removed** (_optional_) `BOOLEAN` removed
  * **logIndex** (_optional_) `STRING` log index
  * **transactionIndex** (_optional_) `STRING` transaction index
  * **transactionHash** `STRING` transaction hash
  * **blockHash** (_optional_) `STRING` block hash
  * **blockNumber** (_optional_) `STRING` block number
  * **address** (_optional_) `STRING` address
  * **data** (_optional_) `STRING` data
  * **topics** (_optional_) topics `ARRAY` of `STRING` 32 hex encoded bytes

### `eth_getLogs`

Returns an array of all logs matching filter with given id.

[Brief version](brief-json-rpc.md#eth\_getLogs)

**PARAMS**

1. **Filter** (_optional_) filter `OBJECT`

* **fromBlock** (_optional_) `STRING` from block
* **toBlock** (_optional_) `STRING` to block
* **address** (_optional_) `ONEOF` of Address(es)
  * `STRING` Address
  * `ARRAY` of `STRING` hex encoded address
*   **topics** (_optional_) Topics `ARRAY` of - `NULL`

    ```
    - `STRING` Single Topic Match

    - `ARRAY` of `STRING` 32 hex encoded bytes
    ```

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getLogs",
  "params": [
    {
      "fromBlock": 7878500,
      "toBlock": 7878700,
      "topics": [
        "0x5445f318f4f5fcfb66592e68e0cc5822aa15664039bd5f0ffde24c5a8142b1ac",
        "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
        "0x0000000000000000000000000000000000000000000000000000000000000000"
      ]
    }
  ]
}
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_getLogs",
  "params": [
    {
      "fromBlock": 7878500,
      "toBlock": 7878700,
      "topics": [
        "0x5445f318f4f5fcfb66592e68e0cc5822aa15664039bd5f0ffde24c5a8142b1ac",
        "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
        "0x0000000000000000000000000000000000000000000000000000000000000000"
      ]
    }
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
  const result = await provider.send("eth_getLogs", [
    {
      fromBlock: 7878500,
      toBlock: 7878700,
      topics: [
        "0x5445f318f4f5fcfb66592e68e0cc5822aa15664039bd5f0ffde24c5a8142b1ac",
        "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
        "0x0000000000000000000000000000000000000000000000000000000000000000",
      ],
    },
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": [
    {
      "address": "0xff39a3e734fe363e631441f6d24c7539240c2628",
      "topics": [
        "0x5445f318f4f5fcfb66592e68e0cc5822aa15664039bd5f0ffde24c5a8142b1ac",
        "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
        "0x0000000000000000000000000000000000000000000000000000000000000000"
      ],
      "data": "0x",
      "blockNumber": "0x7837ac",
      "transactionHash": "0x78c7d04827766c627325d59130b20ccfb3da790785d78f8ab944e2749071aa35",
      "transactionIndex": "0x5f",
      "blockHash": "0xd40899b2216935525b89c16ec2ca1448b82c98bf81bd80abced58977d7c24033",
      "logIndex": "0x74",
      "removed": false
    }
  ]
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Log objects `ONEOF`

* `ARRAY` of `STRING` 32 byte hex value
* `ARRAY` of `STRING` 32 byte hex value
* `ARRAY` of log `OBJECT`
  * **removed** (_optional_) `BOOLEAN` removed
  * **logIndex** (_optional_) `STRING` log index
  * **transactionIndex** (_optional_) `STRING` transaction index
  * **transactionHash** `STRING` transaction hash
  * **blockHash** (_optional_) `STRING` block hash
  * **blockNumber** (_optional_) `STRING` block number
  * **address** (_optional_) `STRING` address
  * **data** (_optional_) `STRING` data
  * **topics** (_optional_) topics `ARRAY` of `STRING` 32 hex encoded bytes

### `eth_mining`

Returns whether the client is actively mining new blocks.

[Brief version](brief-json-rpc.md#eth\_mining)

**PARAMS**

none

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_mining", []);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": false
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Mining status `BOOLEAN` miningStatus

### `eth_hashrate`

Returns the number of hashes per second that the node is mining with.

[Brief version](brief-json-rpc.md#eth\_hashrate)

**PARAMS**

none

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_hashrate", []);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x0"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Mining status `STRING` Hashrate

### `eth_getBalance`

Returns the balance of the account of given address.

[Brief version](brief-json-rpc.md#eth\_getBalance)

**PARAMS**

1. **Address** `STRING` hex encoded address
2. **Block** (_optional_)

* `STRING` Block number
* `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getBalance", [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x0"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Balance `STRING` hex encoded unsigned integer

### `eth_getStorageAt`

Returns the value from a storage position at a given address.

[Brief version](brief-json-rpc.md#eth\_getStorageAt)

**PARAMS**

1. **Address** `STRING` hex encoded address
2. **Storage slot** `STRING` hex encoded unsigned integer
3. **Block** (_optional_)

* `STRING` Block number
* `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getStorageAt", [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "0x0000000000000000000000000000000000000000000000000000000000000001",
    "latest",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x0000000000000000000000000000000000000000000000000000000000000000"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Value `STRING` hex encoded bytes

### `eth_getTransactionCount`

Returns the number of transactions sent from an address.

[Brief version](brief-json-rpc.md#eth\_getTransactionCount)

**PARAMS**

1. **Address** `STRING` hex encoded address
2. **Block** (_optional_)

* `STRING` Block number
* `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getTransactionCount", [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x1"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Transaction count `STRING` hex encoded unsigned integer

### `eth_getCode`

Returns code at a given address.

[Brief version](brief-json-rpc.md#eth\_getCode)

**PARAMS**

1. **Address** `STRING` hex encoded address
2. **Block** (_optional_)

* `STRING` Block number
* `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getCode", [
    "0x05c476a8b9a1a69c47ca81944fbb13a1ac55d62b",
    "latest",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": "0x6080604052600436106100e15760003560e01c806380f59a651161007f578063c01a8c8411610059578063c01a8c8414610349578063c642747414610372578063d0549b851461039b578063ee22610b146103c657610138565b806380f59a65146102a05780639ace38c2146102dd578063a0e67e2b1461031e57610138565b806320ea8d86116100bb57806320ea8d86146101ce5780632e7700f0146101f75780632f54bf6e1461022257806333ea3dc81461025f57610138565b8063025e7c271461013d57806306fdde031461017a5780630bc0fe8f146101a557610138565b36610138573373ffffffffffffffffffffffffffffffffffffffff167f90890809c654f11d6e72a28fa60149770a0d11ec6c92319d6ceb2bb0a4ea1a15344760405161012e929190611704565b60405180910390a2005b600080fd5b34801561014957600080fd5b50610164600480360381019061015f919061176d565b6103ef565b60405161017191906117db565b60405180910390f35b34801561018657600080fd5b5061018f61042e565b60405161019c919061188f565b60405180910390f35b3480156101b157600080fd5b506101cc60048036038101906101c79190611a25565b61046b565b005b3480156101da57600080fd5b506101f560048036038101906101f0919061176d565b61086e565b005b34801561020357600080fd5b5061020c610b48565b6040516102199190611a81565b60405180910390f35b34801561022e57600080fd5b5061024960048036038101906102449190611a9c565b610b55565b6040516102569190611ae4565b60405180910390f35b34801561026b57600080fd5b506102866004803603810190610281919061176d565b610b75565b604051610297959493929190611b54565b60405180910390f35b3480156102ac57600080fd5b506102c760048036038101906102c29190611bae565b610c88565b6040516102d49190611ae4565b60405180910390f35b3480156102e957600080fd5b5061030460048036038101906102ff919061176d565b610cb7565b604051610315959493929190611b54565b60405180910390f35b34801561032a57600080fd5b50610333610db2565b6040516103409190611cac565b60405180910390f35b34801561035557600080fd5b50610370600480360381019061036b919061176d565b610e40565b005b34801561037e57600080fd5b5061039960048036038101906103949190611d83565b61111d565b005b3480156103a757600080fd5b506103b0611327565b6040516103bd9190611a81565b60405180910390f35b3480156103d257600080fd5b506103ed60048036038101906103e8919061176d565b61132d565b005b600181815481106103ff57600080fd5b906000526020600020016000915054906101000a900473ffffffffffffffffffffffffffffffffffffffff1681565b60606040518060400160405280600e81526020017f4d756c746953696757616c6c6574000000000000000000000000000000000000815250905090565b60008060019054906101000a900460ff1615905080801561049c5750600160008054906101000a900460ff1660ff16105b806104c957506104ab30611625565b1580156104c85750600160008054906101000a900460ff1660ff16145b5b610508576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016104ff90611e64565b60405180910390fd5b60016000806101000a81548160ff021916908360ff1602179055508015610545576001600060016101000a81548160ff0219169083151502179055505b7f63a242a632efe33c0e210e04e4173612a17efa4f16aa4890bc7e46caece80de0600a6040516105759190611ec9565b60405180910390a160008351116105c1576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016105b890611f30565b60405180910390fd5b6000821180156105d2575082518211155b610611576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040161060890611fc2565b60405180910390fd5b60005b835181101561080857600084828151811061063257610631611fe2565b5b60200260200101519050600073ffffffffffffffffffffffffffffffffffffffff168173ffffffffffffffffffffffffffffffffffffffff1614156106ac576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016106a39061205d565b60405180910390fd5b600260008273ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff1615610739576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401610730906120c9565b60405180910390fd5b6001600260008373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81548160ff0219169083151502179055506001819080600181540180825580915050600190039060005260206000200160009091909190916101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff16021790555050808061080090612118565b915050610614565b508160038190555080156108695760008060016101000a81548160ff0219169083151502179055507f7f26b83ff96e1f2b6a682f133852f6798a09c465da95921460cefb3847402498600160405161086091906121a9565b60405180910390a15b505050565b600260003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff166108fa576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016108f190612210565b60405180910390fd5b806005805490508110610942576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016109399061227c565b60405180910390fd5b816005818154811061095757610956611fe2565b5b906000526020600020906005020160030160009054906101000a900460ff16156109b6576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016109ad906122e8565b60405180910390fd5b6000600584815481106109cc576109cb611fe2565b5b906000526020600020906005020190506004600085815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff16610a79576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401610a7090612354565b60405180910390fd5b6001816004016000828254610a8e9190612374565b9250508190555060006004600086815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81548160ff021916908315150217905550833373ffffffffffffffffffffffffffffffffffffffff167fc423fd18c78c483f167229efa90b29abe30eed1425ab9cb40441f6555650eca860405160405180910390a350505050565b6000600580549050905090565b60026020528060005260406000206000915054906101000a900460ff1681565b6000806060600080600060058781548110610b9357610b92611fe2565b5b906000526020600020906005020190508060000160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff168160010154826002018360030160009054906101000a900460ff168460040154828054610bf4906123d7565b80601f0160208091040260200160405190810160405280929190818152602001828054610c20906123d7565b8015610c6d5780601f10610c4257610100808354040283529160200191610c6d565b820191906000526020600020905b815481529060010190602001808311610c5057829003601f168201915b50505050509250955095509550955095505091939590929450565b60046020528160005260406000206020528060005260406000206000915091509054906101000a900460ff1681565b60058181548110610cc757600080fd5b90600052602060002090600502016000915090508060000160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1690806001015490806002018054610d16906123d7565b80601f0160208091040260200160405190810160405280929190818152602001828054610d42906123d7565b8015610d8f5780601f10610d6457610100808354040283529160200191610d8f565b820191906000526020600020905b815481529060010190602001808311610d7257829003601f168201915b5050505050908060030160009054906101000a900460ff16908060040154905085565b60606001805480602002602001604051908101604052809291908181526020018280548015610e3657602002820191906000526020600020905b8160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019060010190808311610dec575b5050505050905090565b600260003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff16610ecc576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401610ec390612210565b60405180910390fd5b806005805490508110610f14576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401610f0b9061227c565b60405180910390fd5b8160058181548110610f2957610f28611fe2565b5b906000526020600020906005020160030160009054906101000a900460ff1615610f88576040517f08c379a0000000000000000000000000000000000000000000000000000000008152600401610f7f906122e8565b60405180910390fd5b826004600082815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff1615611027576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040161101e90612455565b60405180910390fd5b60006005858154811061103d5761103c611fe2565b5b9060005260206000209060050201905060018160040160008282546110629190612475565b9250508190555060016004600087815260200190815260200160002060003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060006101000a81548160ff021916908315150217905550843373ffffffffffffffffffffffffffffffffffffffff167f52a3954c699324c8e90e7e2f7cb9f57cd61af1902197bafcc5085b6c2a57b82360405160405180910390a35050505050565b600260003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff166111a9576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016111a090612210565b60405180910390fd5b6000600580549050905060056040518060a001604052808673ffffffffffffffffffffffffffffffffffffffff1681526020018581526020018481526020016000151581526020016000815250908060018154018082558091505060019003906000526020600020906005020160009091909190915060008201518160000160006101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff16021790555060208201518160010155604082015181600201908051906020019061128c929190611648565b5060608201518160030160006101000a81548160ff0219169083151502179055506080820151816004015550508373ffffffffffffffffffffffffffffffffffffffff16813373ffffffffffffffffffffffffffffffffffffffff167f52e5c631bb2fd786d6b1c26f68548e07c61d087bf325770dd88d072cf0a5e8b086866040516113199291906124cb565b60405180910390a450505050565b60035481565b600260003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060009054906101000a900460ff166113b9576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016113b090612210565b60405180910390fd5b806005805490508110611401576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016113f89061227c565b60405180910390fd5b816005818154811061141657611415611fe2565b5b906000526020600020906005020160030160009054906101000a900460ff1615611475576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040161146c906122e8565b60405180910390fd5b60006005848154811061148b5761148a611fe2565b5b90600052602060002090600502019050600354816004015410156114e4576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016114db90612547565b60405180910390fd5b60018160030160006101000a81548160ff02191690831515021790555060008160000160009054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168260010154836002016040516115549190612606565b60006040518083038185875af1925050503d8060008114611591576040519150601f19603f3d011682016040523d82523d6000602084013e611596565b606091505b50509050806115da576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016115d190612669565b60405180910390fd5b843373ffffffffffffffffffffffffffffffffffffffff167f5445f318f4f5fcfb66592e68e0cc5822aa15664039bd5f0ffde24c5a8142b1ac60405160405180910390a35050505050565b6000808273ffffffffffffffffffffffffffffffffffffffff163b119050919050565b828054611654906123d7565b90600052602060002090601f01602090048101928261167657600085556116bd565b82601f1061168f57805160ff19168380011785556116bd565b828001600101855582156116bd579182015b828111156116bc5782518255916020019190600101906116a1565b5b5090506116ca91906116ce565b5090565b5b808211156116e75760008160009055506001016116cf565b5090565b6000819050919050565b6116fe816116eb565b82525050565b600060408201905061171960008301856116f5565b61172660208301846116f5565b9392505050565b6000604051905090565b600080fd5b600080fd5b61174a816116eb565b811461175557600080fd5b50565b60008135905061176781611741565b92915050565b60006020828403121561178357611782611737565b5b600061179184828501611758565b91505092915050565b600073ffffffffffffffffffffffffffffffffffffffff82169050919050565b60006117c58261179a565b9050919050565b6117d5816117ba565b82525050565b60006020820190506117f060008301846117cc565b92915050565b600081519050919050565b600082825260208201905092915050565b60005b83811015611830578082015181840152602081019050611815565b8381111561183f576000848401525b50505050565b6000601f19601f8301169050919050565b6000611861826117f6565b61186b8185611801565b935061187b818560208601611812565b61188481611845565b840191505092915050565b600060208201905081810360008301526118a98184611856565b905092915050565b600080fd5b7f4e487b7100000000000000000000000000000000000000000000000000000000600052604160045260246000fd5b6118ee82611845565b810181811067ffffffffffffffff8211171561190d5761190c6118b6565b5b80604052505050565b600061192061172d565b905061192c82826118e5565b919050565b600067ffffffffffffffff82111561194c5761194b6118b6565b5b602082029050602081019050919050565b600080fd5b61196b816117ba565b811461197657600080fd5b50565b60008135905061198881611962565b92915050565b60006119a161199c84611931565b611916565b905080838252602082019050602084028301858111156119c4576119c361195d565b5b835b818110156119ed57806119d98882611979565b8452602084019350506020810190506119c6565b5050509392505050565b600082601f830112611a0c57611a0b6118b1565b5b8135611a1c84826020860161198e565b91505092915050565b60008060408385031215611a3c57611a3b611737565b5b600083013567ffffffffffffffff811115611a5a57611a5961173c565b5b611a66858286016119f7565b9250506020611a7785828601611758565b9150509250929050565b6000602082019050611a9660008301846116f5565b92915050565b600060208284031215611ab257611ab1611737565b5b6000611ac084828501611979565b91505092915050565b60008115159050919050565b611ade81611ac9565b82525050565b6000602082019050611af96000830184611ad5565b92915050565b600081519050919050565b600082825260208201905092915050565b6000611b2682611aff565b611b308185611b0a565b9350611b40818560208601611812565b611b4981611845565b840191505092915050565b600060a082019050611b6960008301886117cc565b611b7660208301876116f5565b8181036040830152611b888186611b1b565b9050611b976060830185611ad5565b611ba460808301846116f5565b9695505050505050565b60008060408385031215611bc557611bc4611737565b5b6000611bd385828601611758565b9250506020611be485828601611979565b9150509250929050565b600081519050919050565b600082825260208201905092915050565b6000819050602082019050919050565b611c23816117ba565b82525050565b6000611c358383611c1a565b60208301905092915050565b6000602082019050919050565b6000611c5982611bee565b611c638185611bf9565b9350611c6e83611c0a565b8060005b83811015611c9f578151611c868882611c29565b9750611c9183611c41565b925050600181019050611c72565b5085935050505092915050565b60006020820190508181036000830152611cc68184611c4e565b905092915050565b600080fd5b600067ffffffffffffffff821115611cee57611ced6118b6565b5b611cf782611845565b9050602081019050919050565b82818337600083830152505050565b6000611d26611d2184611cd3565b611916565b905082815260208101848484011115611d4257611d41611cce565b5b611d4d848285611d04565b509392505050565b600082601f830112611d6a57611d696118b1565b5b8135611d7a848260208601611d13565b91505092915050565b600080600060608486031215611d9c57611d9b611737565b5b6000611daa86828701611979565b9350506020611dbb86828701611758565b925050604084013567ffffffffffffffff811115611ddc57611ddb61173c565b5b611de886828701611d55565b9150509250925092565b7f496e697469616c697a61626c653a20636f6e747261637420697320616c72656160008201527f647920696e697469616c697a6564000000000000000000000000000000000000602082015250565b6000611e4e602e83611801565b9150611e5982611df2565b604082019050919050565b60006020820190508181036000830152611e7d81611e41565b9050919050565b6000819050919050565b6000819050919050565b6000611eb3611eae611ea984611e84565b611e8e565b6116eb565b9050919050565b611ec381611e98565b82525050565b6000602082019050611ede6000830184611eba565b92915050565b7f6f776e6572732072657175697265640000000000000000000000000000000000600082015250565b6000611f1a600f83611801565b9150611f2582611ee4565b602082019050919050565b60006020820190508181036000830152611f4981611f0d565b9050919050565b7f696e76616c6964206e756d626572206f6620726571756972656420636f6e666960008201527f726d6174696f6e73000000000000000000000000000000000000000000000000602082015250565b6000611fac602883611801565b9150611fb782611f50565b604082019050919050565b60006020820190508181036000830152611fdb81611f9f565b9050919050565b7f4e487b7100000000000000000000000000000000000000000000000000000000600052603260045260246000fd5b7f696e76616c6964206f776e657200000000000000000000000000000000000000600082015250565b6000612047600d83611801565b915061205282612011565b602082019050919050565b600060208201905081810360008301526120768161203a565b9050919050565b7f6f776e6572206e6f7420756e6971756500000000000000000000000000000000600082015250565b60006120b3601083611801565b91506120be8261207d565b602082019050919050565b600060208201905081810360008301526120e2816120a6565b9050919050565b7f4e487b7100000000000000000000000000000000000000000000000000000000600052601160045260246000fd5b6000612123826116eb565b91507fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff821415612156576121556120e9565b5b600182019050919050565b6000819050919050565b600060ff82169050919050565b600061219361218e61218984612161565b611e8e565b61216b565b9050919050565b6121a381612178565b82525050565b60006020820190506121be600083018461219a565b92915050565b7f6e6f74206f776e65720000000000000000000000000000000000000000000000600082015250565b60006121fa600983611801565b9150612205826121c4565b602082019050919050565b60006020820190508181036000830152612229816121ed565b9050919050565b7f747820646f6573206e6f74206578697374000000000000000000000000000000600082015250565b6000612266601183611801565b915061227182612230565b602082019050919050565b6000602082019050818103600083015261229581612259565b9050919050565b7f747820616c726561647920657865637574656400000000000000000000000000600082015250565b60006122d2601383611801565b91506122dd8261229c565b602082019050919050565b60006020820190508181036000830152612301816122c5565b9050919050565b7f7478206e6f7420636f6e6669726d656400000000000000000000000000000000600082015250565b600061233e601083611801565b915061234982612308565b602082019050919050565b6000602082019050818103600083015261236d81612331565b9050919050565b600061237f826116eb565b915061238a836116eb565b92508282101561239d5761239c6120e9565b5b828203905092915050565b7f4e487b7100000000000000000000000000000000000000000000000000000000600052602260045260246000fd5b600060028204905060018216806123ef57607f821691505b60208210811415612403576124026123a8565b5b50919050565b7f747820616c726561647920636f6e6669726d6564000000000000000000000000600082015250565b600061243f601483611801565b915061244a82612409565b602082019050919050565b6000602082019050818103600083015261246e81612432565b9050919050565b6000612480826116eb565b915061248b836116eb565b9250827fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff038211156124c0576124bf6120e9565b5b828201905092915050565b60006040820190506124e060008301856116f5565b81810360208301526124f28184611b1b565b90509392505050565b7f63616e6e6f742065786563757465207478000000000000000000000000000000600082015250565b6000612531601183611801565b915061253c826124fb565b602082019050919050565b6000602082019050818103600083015261256081612524565b9050919050565b600081905092915050565b60008190508160005260206000209050919050565b60008154612594816123d7565b61259e8186612567565b945060018216600081146125b957600181146125ca576125fd565b60ff198316865281860193506125fd565b6125d385612572565b60005b838110156125f5578154818901526001820191506020810190506125d6565b838801955050505b50505092915050565b60006126128284612587565b915081905092915050565b7f7478206661696c65640000000000000000000000000000000000000000000000600082015250565b6000612653600983611801565b915061265e8261261d565b602082019050919050565b6000602082019050818103600083015261268281612646565b905091905056fea26469706673582212206c9d550f615a6cc987e89a94b4f4b6d7be4c8c2da4ace7b55292611c528f9a8864736f6c63430008090033"
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Bytecode `STRING` hex encoded bytes

### ~~`eth_sendTransaction`~~

Tenderly doesn't store private keys, so this method is not supported

### `eth_sendRawTransaction`

Submits a raw transaction.

[Brief version](brief-json-rpc.md#eth\_sendRawTransaction)

**PARAMS**

1. **Transaction** `STRING` hex encoded bytes

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_sendRawTransaction",
  "params": [
    "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"
  ]
}
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "eth_sendRawTransaction",
  "params": [
    "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"
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
  const result = await provider.send("eth_sendRawTransaction", [
    "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675"
  ]);

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

**RESULT**: Transaction hash `STRING` 32 byte hex value

### `eth_getTransactionByHash`

Returns the information about a transaction requested by transaction hash.

[Brief version](brief-json-rpc.md#eth\_getTransactionByHash)

**PARAMS**

1. **Transaction hash** `STRING` 32 byte hex value

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getTransactionByHash", [
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "blockHash": "0xb39de02094847558d1b5b7be17899af87d4026419f063946d347aeb4b8f17b56",
    "blockNumber": "0x7787e4",
    "transactionIndex": "0x24",
    "hash": "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188",
    "from": "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
    "to": "0xd9ded92319814d8f3587dfad7be72ca71e16697a",
    "input": "0xee22610b0000000000000000000000000000000000000000000000000000000000000000",
    "nonce": "0x17",
    "value": "0x0",
    "gas": "0xf4240",
    "gasPrice": "0x9a26693e",
    "maxPriorityFeePerGas": "0x59682f00",
    "maxFeePerGas": "0xab58f0b6",
    "accessList": [],
    "chainId": "0x5",
    "type": "0x2",
    "v": "0x1",
    "r": "0x1a54710a2409beff5e5726830497f9f56f0ae1545c25b4436d8ac8d68900c2e8",
    "s": "0x5b6b60bbb030b1f88d098252d98b4731d7e89d6b1a8b2e7dee61c2ea45866f29"
  }
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Transaction information Transaction information `OBJECT`

* **blockHash** `STRING` block hash
* **blockNumber** `STRING` block number
* **from** `STRING` from address
* **hash** `STRING` transaction hash
* **transactionIndex** `STRING` transaction index

### `eth_getTransactionByBlockHashAndIndex`

Returns information about a transaction by block hash and transaction index position.

[Brief version](brief-json-rpc.md#eth\_getTransactionByBlockHashAndIndex)

**PARAMS**

1. **Block hash** `STRING` 32 byte hex value
2. **Transaction index** `STRING` hex encoded unsigned integer

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getTransactionByBlockHashAndIndex", [
    "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    "0x1",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "blockHash": "0x5a10754ae6c673ebabb1a78166232c6b88633d50fafe1499392dd6e4c61c344e",
    "blockNumber": "0x77ed36",
    "transactionIndex": "0x1",
    "hash": "0x08f23a8d29dc0b23989b648f11fd89fad609c6694305b5d35e9b6d5fe1616d3a",
    "from": "0x22841539c4c3a3fa3c1355db7352adfb3a699ada",
    "to": null,
    "input": "0x608060405273b3cb14c326da065d8987e9ef4d771d758dad42a76000806101000a81548173ffffffffffffffffffffffffffffffffffffffff021916908373ffffffffffffffffffffffffffffffffffffffff16021790555034801561006457600080fd5b50610196806100746000396000f3fe608060405234801561001057600080fd5b506004361061002b5760003560e01c80639e5faafc14610030575b600080fd5b61003861004e565b6040518082815260200191505060405180910390f35b60008067ffffffff0000ffff60c01b3360601b16905060005b611fff811161015a5760008054906101000a900473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16633370204e826201388001846040518363ffffffff1660e01b8152600401808277ffffffffffffffffffffffffffffffffffffffffffffffff19168152602001915050602060405180830381600088803b15801561010457600080fd5b5087f19350505050801561013957506040513d602081101561012557600080fd5b810190808051906020019092919050505060015b6101425761014d565b50809250505061015d565b8080600101915050610067565b50505b9056fea26469706673582212201082b38baaf4aa56ba1dbf14484c0ecabd8ba0cfb25a9b73905c51f3740d8bdb64736f6c634300060c0033",
    "nonce": "0x85",
    "value": "0x0",
    "gas": "0x282ac",
    "gasPrice": "0x9502f910",
    "maxPriorityFeePerGas": "0x9502f900",
    "maxFeePerGas": "0x9502f920",
    "accessList": [],
    "chainId": "0x5",
    "type": "0x2",
    "v": "0x0",
    "r": "0x1e4c8de7ea1e201d509144f8d081100db747267738c4f4b0e649cda6886f1e4c",
    "s": "0x6177915db9f2b5cd103bcf528a66cdad152f2394eabe42c0d357cd4c45600154"
  }
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Transaction information Transaction information `OBJECT`

* **blockHash** `STRING` block hash
* **blockNumber** `STRING` block number
* **from** `STRING` from address
* **hash** `STRING` transaction hash
* **transactionIndex** `STRING` transaction index

### `eth_getTransactionByBlockNumberAndIndex`

Returns information about a transaction by block number and transaction index position.

[Brief version](brief-json-rpc.md#eth\_getTransactionByBlockNumberAndIndex)

**PARAMS**

1. **Block**

* `STRING` Block number
* `ENUM` of Block tag `earliest|finalized|safe|latest|pending`

1. **Transaction index** `STRING` hex encoded unsigned integer

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send(
    "eth_getTransactionByBlockNumberAndIndex",
    ["latest", "0x1"]
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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "blockHash": "0xd65ea6ed7a1204d48c3f172aa052efabf1e3ebfbab251e5ffb55e2cac8b511d5",
    "blockNumber": "0x7aa3a9",
    "transactionIndex": "0x1",
    "hash": "0x052242bf239f5fc8b5bb2f156cf22ef6ce2eb738304ba3a7d5998c15d2a97140",
    "from": "0x8b8a3c7b9a182f3176885cf4c72ac53271eb9d7e",
    "to": "0x4569d6f9548aa47f4f4b9795339c0ea1d1610278",
    "input": "0x",
    "nonce": "0x12509",
    "value": "0x2c68af0bb140000",
    "gas": "0xf618",
    "gasPrice": "0x51a03641c",
    "accessList": [],
    "chainId": "0x5",
    "type": "0x0",
    "v": "0x2e",
    "r": "0x784f52eddf2746ee8605607db4d8aad97186653b9789f81de4b462befbd63b39",
    "s": "0x5c095cba9a6c77c1492ccb5a077fa63e7115d5c01ac33659826fbe6aee5a142a"
  }
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Transaction information Transaction information `OBJECT`

* **blockHash** `STRING` block hash
* **blockNumber** `STRING` block number
* **from** `STRING` from address
* **hash** `STRING` transaction hash
* **transactionIndex** `STRING` transaction index

### `eth_getTransactionReceipt`

Returns the receipt of a transaction by transaction hash.

[Brief version](brief-json-rpc.md#eth\_getTransactionReceipt)

**PARAMS**

1. **Transaction hash** (_optional_) `STRING` 32 byte hex value

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
curl https://goerli.gateway.tenderly.co/$TENDERLY_NODE_KEY \
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
  const result = await provider.send("eth_getTransactionReceipt", [
    "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188",
  ]);

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
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "type": "0x2",
    "status": "0x1",
    "cumulativeGasUsed": "0x65f9a6",
    "logsBloom": "0x02000008000000000000000000000000000000000000000000000004000000000000000000000000000000004000000000000000000000400000000000000000000000000000000000000000000000000000000000000000000000000000000040000000020000000000000000000800000000000000000000000000000000000000000000000000000000000000000000000080000000000000000000000008000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000008000000000",
    "logs": [
      {
        "address": "0xd9ded92319814d8f3587dfad7be72ca71e16697a",
        "topics": [
          "0x5445f318f4f5fcfb66592e68e0cc5822aa15664039bd5f0ffde24c5a8142b1ac",
          "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
          "0x0000000000000000000000000000000000000000000000000000000000000000"
        ],
        "data": "0x",
        "blockNumber": "0x7787e4",
        "transactionHash": "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188",
        "transactionIndex": "0x24",
        "blockHash": "0xb39de02094847558d1b5b7be17899af87d4026419f063946d347aeb4b8f17b56",
        "logIndex": "0x55",
        "removed": false
      }
    ],
    "transactionHash": "0xd9724b68ad04ac3919678e3158f5d474d3c129cfb4cb7fafcde9b4c756fce188",
    "from": "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
    "to": "0xd9ded92319814d8f3587dfad7be72ca71e16697a",
    "contractAddress": null,
    "gasUsed": "0x19280",
    "effectiveGasPrice": "0x9a26693e",
    "blockHash": "0xb39de02094847558d1b5b7be17899af87d4026419f063946d347aeb4b8f17b56",
    "blockNumber": "0x7787e4",
    "transactionIndex": "0x24"
  }
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Receipt Information Receipt info `OBJECT`

* **transactionHash** `STRING` transaction hash
* **transactionIndex** `STRING` transaction index
* **blockHash** `STRING` block hash
* **blockNumber** `STRING` block number
* **from** `STRING` from
* **to** (_optional_) `STRING` to: Address of the receiver or null in a contract creation transaction.
* **cumulativeGasUsed** `STRING` cumulative gas used: The sum of gas used by this transaction and all preceding transactions in the same block.
* **gasUsed** `STRING` gas used: The amount of gas used for this specific transaction alone.
* **contractAddress** (_optional_) `ONEOF` of contract address: The contract address created, if the transaction was a contract creation, otherwise null.
  * `STRING` hex encoded address
  * `NULL`
* **logs** logs `ARRAY` of log `OBJECT`
  * **removed** (_optional_) `BOOLEAN` removed
  * **logIndex** (_optional_) `STRING` log index
  * **transactionIndex** (_optional_) `STRING` transaction index
  * **transactionHash** `STRING` transaction hash
  * **blockHash** (_optional_) `STRING` block hash
  * **blockNumber** (_optional_) `STRING` block number
  * **address** (_optional_) `STRING` address
  * **data** (_optional_) `STRING` data
  * **topics** (_optional_) topics `ARRAY` of `STRING` 32 hex encoded bytes
* **logsBloom** `STRING` logs bloom
* **root** (_optional_) `STRING` state root: The post-transaction state root. Only specified for transactions included before the Byzantium upgrade.
* **status** (_optional_) `STRING` status: Either 1 (success) or 0 (failure). Only specified for transactions included after the Byzantium upgrade.
* **effectiveGasPrice** `STRING` effective gas price: The actual value per gas deducted from the senders account. Before EIP-1559, this is equal to the transaction's gas price. After, it is equal to baseFeePerGas + min(maxFeePerGas - baseFeePerGas, maxPriorityFeePerGas).



### `eth_subscribe`

Subscribes user to a Ethereum event notification stream.

[Brief version](brief-json-rpc.md#eth\_subscribe)

**PARAMS**

1. **Event type** `STRING`

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "eth_subscribe",
  "params": ["newHeads"]
}
```
{% endtab %}

{% tab title="wscat" %}
```bash
# Initialize websocket stream
wscat -c wss://mainnet.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY

# Send JSON request
{"jsonrpc":"2.0","id": 2, "method": "eth_subscribe", "params": ["newHeads"]}
```
{% endtab %}

{% tab title="Response" %}
<pre class="language-json"><code class="lang-json"><strong>{
</strong>  "jsonrpc":"2.0",
  "id":1,
  "result":"0x4a8a4c0517381924f9838102c5a4dcb7"
}
</code></pre>
{% endtab %}
{% endtabs %}

Supported events are listed in the following table.

<table><thead><tr><th width="235">Event type</th><th>Description</th><th data-hidden></th></tr></thead><tbody><tr><td>newHeads</td><td>Fires a notification each time a new header is appended to the chain, including chain reorganisations.</td><td></td></tr><tr><td>logs</td><td>Returns logs that are included in new imported blocks and match the given filter criteria.</td><td></td></tr><tr><td>newPendingTransaction</td><td>Returns the hash for transactions that are added to the pending state.</td><td></td></tr><tr><td>syncing</td><td>Indicates when the node starts or stops synchronising.</td><td></td></tr></tbody></table>



2. **Filter** `JSON object`

This parameter have effect only if subscription type is set to `logs`. User can filter logs that match given address and one of several topics listed in the filter.

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "eth_subscribe",
  "params": [
    "logs",
    {
      "address": "0x8320fe7702b96808f7bbc0d4a888ed1468216cfd",
      "topics": ["0xd78a0cb8bb633d06981248b816e7bd33c2a35a6089241d099fa519e361cab902"]
    }
  ]
}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "jsonrpc":"2.0",
  "id":1,
  "result":"0x4a8a4c0517381924f9838102c5a4dcb7"
}
```
{% endtab %}
{% endtabs %}



**RESULT**: Subscription ID `Hex value`

```json
{
  "jsonrpc":"2.0",
  "id":1,
  "result":"0x4a8a4c0517381924f9838102c5a4dcb7"
}
```



#### Notifications

`eth_subscribe` should only be used over a websocket connections. After the subscription is established, the same websocket connection will be used to send notifications.

Notifications are JSON objects. The objects have different form for different event types. Examples for each event type follows.

New head notification.

```json
{
  "jsonrpc": "2.0",
  "method": "eth_subscription",
  "params": {
    "result": {
      "difficulty": "0x15d9223a23aa",
      "extraData": "0xd983010305844765746887676f312e342e328777696e646f7773",
      "gasLimit": "0x47e7c4",
      "gasUsed": "0x38658",
      "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
      "miner": "0xf8b483dba2c3b7176a3da549ad41a48bb3121069",
      "nonce": "0x084149998194cc5f",
      "number": "0x1348c9",
      "parentHash": "0x7736fab79e05dc611604d22470dadad26f56fe494421b5b333de816ce1f25701",
      "receiptRoot": "0x2fab35823ad00c7bb388595cb46652fe7886e00660a01e867824d3dceb1c8d36",
      "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
      "stateRoot": "0xb3346685172db67de536d8765c43c31009d0eb3bd9c501c9be3229203f15f378",
      "timestamp": "0x56ffeff8",
      "transactionsRoot": "0x0167ffa60e3ebc0b080cdb95f7c0087dd6c0e61413140e39d94d3468d7c9689f"
    },
    "subscription": "0x9ce59a13059e417087c02d3236a0b1cc"
  }
}
```

Logs notification.

```json
{
  "jsonrpc": "2.0",
  "method": "eth_subscription",
  "params": {
    "subscription": "0x4a8a4c0517381924f9838102c5a4dcb7",
    "result": {
      "address": "0x8320fe7702b96808f7bbc0d4a888ed1468216cfd",
      "blockHash": "0x61cdb2a09ab99abf791d474f20c2ea89bf8de2923a2d42bb49944c8c993cbf04",
      "blockNumber": "0x29e87",
      "data": "0x00000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000003",
      "logIndex": "0x0",
      "topics": [
        "0xd78a0cb8bb633d06981248b816e7bd33c2a35a6089241d099fa519e361cab902"
      ],
      "transactionHash": "0xe044554a0a55067caafd07f8020ab9f2af60bdfe337e395ecd84b4877a3d1ab4",
      "transactionIndex": "0x0"
    }
  }
}
```

New pending transaction notification.

```json
{
  "jsonrpc":"2.0",
  "method":"eth_subscription",
  "params":{
    "subscription":"0xc3b33aa549fb9a60e95d21862596617c",
    "result":"0xd6fdc5cc41a9959e922f30cb772a9aef46f4daea279307bc5f7024edc4ccd7fa"
  }
}
```

Sync notification.

```json
{
    "subscription": "0xe2ffeb2703bcf602d42922385829ce96",
    "result": {
        "syncing": false
    }
}
```



### `eth_unsubscribe`

Unsubscribes user from a previously subscribed Ethereum event notification stream.

[Brief version](detailed-json-rpc.md#eth\_unsubscribe)

**PARAMS**

1. **Subscription ID** `STRING that represents hex value`

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "eth_unsubscribe",
  "params": ["0x9cef478923ff08bf67fde6c64013158d"]
}
```
{% endtab %}

{% tab title="wscat" %}
```bash
# Initialize websocket stream
wscat -c wss://mainnet.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY

# Send JSON request
{"jsonrpc":"2.0","id": 2, "method": "eth_unsubscribe", "params": ["0x9cef478923ff08bf67fde6c64013158d"]}
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "jsonrpc":"2.0",
  "id":1,
  "result":true
}
```
{% endtab %}
{% endtabs %}

**RESULT**: `Boolean` Flag that represents if unsubscribe call is successful

```json
{
  "jsonrpc":"2.0",
  "id":1,
  "result":true
}
```

Note: eth\_unsubscribe have to be issued on the websocket connection previously used to establish the subscription.

