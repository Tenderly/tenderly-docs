---
description: >-
  Learn more about the Tenderly Transaction Simulation endpoints, featuring
  detailed requests, responses, and example payloads.
---

# Tenderly Simulation API

## Simulate a transaction

This endpoint allows you to simulate a transaction with different parameters on any of [30+ networks](../../supported-networks-and-languages.md) supported by Tenderly. The simulation output shows the emitted events and state changes that this transaction might cause if you sent it to the blockchain.

### Endpoint

```bash
POST https://api.tenderly.co/api/v1/account/{{accountID}}/project/{{projectID}}/simulate
```

### Request Payload

Transaction request payload with fields and explanation:

<table><thead><tr><th width="195">Field</th><th width="105">Type</th><th width="167">Description</th><th width="120">Mandatory</th><th>Example Value</th></tr></thead><tbody><tr><td><strong>network_id</strong></td><td>string</td><td>ID of the network on which the simulation is being run.</td><td>Yes</td><td>“1”</td></tr><tr><td><strong>block_number</strong></td><td>number</td><td>Number of the block to be used for the simulation.</td><td>Yes</td><td>17884230</td></tr><tr><td><strong>transaction_index</strong></td><td>number</td><td>Index of the transaction within the block.</td><td>No</td><td>0</td></tr><tr><td><strong>from</strong></td><td>string</td><td>Address initiating the transaction.</td><td>Yes</td><td>“0x3f41a1cfd3c8b8d9c162de0f42307a0095a6e5df”</td></tr><tr><td><strong>input</strong></td><td>string</td><td>Encoded contract method call data.</td><td>Yes</td><td>“0x…”</td></tr><tr><td><strong>to</strong></td><td>string</td><td>The recipient address of the transaction.</td><td>Yes</td><td>“0xdef171fe48cf0115b1d80b88dc8eab59176fee57”</td></tr><tr><td><strong>gas</strong></td><td>number</td><td>Amount of gas provided for the simulation.</td><td>Yes</td><td>648318</td></tr><tr><td><strong>gas_price</strong></td><td>string</td><td>Price of the gas in Wei.</td><td>No</td><td>“18312000018”</td></tr><tr><td><strong>value</strong></td><td>string</td><td>Amount of Ether (in Wei) sent along with the transaction.</td><td>No</td><td>“0”</td></tr><tr><td><strong>access_list</strong></td><td>Object</td><td>List of addresses with their storage keys to grant access for this transaction.</td><td>No</td><td>[{"address": "0x3f41a1cfd3c8b8d9c162de0f42307a0095a6e5df", "storage_keys": [] }]</td></tr><tr><td><strong>save</strong></td><td>boolean</td><td>Flag indicating whether to save the simulation in dashboard UI.</td><td>No</td><td>true</td></tr><tr><td><strong>save_if_fails</strong></td><td>boolean</td><td>Flag indicating whether to save failed simulation in dashboard UI.</td><td>No</td><td>true</td></tr><tr><td><strong>simulation_type</strong></td><td>string</td><td>Opt for quick, abi, or full simulation API mode.</td><td>No</td><td>“full”</td></tr><tr><td><strong>block_header</strong></td><td>Object</td><td>Details of the block header based on the provided block number.</td><td>No</td><td>{ "number": "0x110ace7", "hash": "0x0000000000000000000000000000000000000000000000000000000000000000", // ... }</td></tr><tr><td><strong>state_objects</strong></td><td>Object</td><td>Overrides for specific state objects.</td><td>No</td><td>"0xdac17f958d2ee523a2206206994597c13d831ec7": { "storage": { "0x0000000000000000000000000000000000000000000000000000000000000000": "0x000000000000000000000000c6cde7c39eb2f0f0095f41570af89efc2c1ea828" } }</td></tr></tbody></table>

### Request Payload Example

Below you can find request payload examples. Replace `TENDERLY_ACCOUNT_NAME` and `TENDERLY_PROJECT_NAME` with appropriate values using our [platform access](https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name) guide.

{% tabs %}
{% tab title="fetch" %}
```javascript
await fetch("https://api.tenderly.co/api/v1/account/{{TENDERLY_ACCOUNT_NAME}}/project/{{TENDERLY_PROJECT_NAME}}/simulate", {
  "headers": {
    "authorization": "Bearer <TOKEN>",
    "content-type": "application/json"
  },
  "body": "{\"network_id\":\"1\",\"block_number\":17913717,\"transaction_index\":0,\"from\":\"0x0000000000000000000000000000000000000000\",\"input\":\"0x9dc29fac0000000000000000000000003ec7ef9b96a36faa0c0949a2ba804f60d12593dd000000000000000000000000000000000000000000000000000133c2207c0ede\",\"to\":\"0x6b175474e89094c44da98b954eedeac495271d0f\",\"gas\":30000000,\"gas_price\":\"0\",\"value\":\"0\",\"access_list\":[],\"generate_access_list\":true,\"save\":true,\"block_header\":{\"number\":\"0x1115775\",\"hash\":\"0x0000000000000000000000000000000000000000000000000000000000000000\",\"stateRoot\":\"0x0000000000000000000000000000000000000000000000000000000000000000\",\"parentHash\":\"0xcf515aa3543ac1129b9bb2c140e419427b9edd2c516bbfa5754d4ae7368acade\",\"sha3Uncles\":\"0x0000000000000000000000000000000000000000000000000000000000000000\",\"transactionsRoot\":\"0x0000000000000000000000000000000000000000000000000000000000000000\",\"receiptsRoot\":\"0x0000000000000000000000000000000000000000000000000000000000000000\",\"logsBloom\":\"0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000\",\"timestamp\":\"0x64da3b8a\",\"difficulty\":\"0x0\",\"gasLimit\":\"0x1c9c380\",\"gasUsed\":\"0x123b15e\",\"baseFeePerGas\":\"0x1\",\"miner\":\"0x690b9a9e9aa1c9db991c7721a92d351db4fac990\",\"extraData\":\"0x\",\"mixHash\":\"0x0000000000000000000000000000000000000000000000000000000000000000\",\"nonce\":\"0x0000000000000000\",\"size\":\"0x0\",\"totalDifficulty\":\"0x0\",\"transactions\":null,\"uncles\":null}}",
  "method": "POST"
});
```
{% endtab %}

{% tab title="cURL" %}
{% code lineNumbers="true" %}
```bash
curl 'https://api.tenderly.co/api/v1/account/{{TENDERLY_ACCOUNT_NAME}}/project/{{TENDERLY_PROJECT_NAME}}/simulate' \
  -H 'authorization: Bearer <TOKEN>' \
  -H 'content-type: application/json' \
  --data-raw '{"network_id":"1","block_number":17884583,"transaction_index":0,"from":"0x3f41a1cfd3c8b8d9c162de0f42307a0095a6e5df","input":"0xa94e78ef000000000000000000000000000000000000000000000000000000000000002000000000000000000000000068037790a0229e9ce6eaa8a99ea92964106c470300000000000000000000000000000000000000000000010f0cf064dd592000000000000000000000000000000000000000000000000000000000000145dc1b2e00000000000000000000000000000000000000000000000000000001477f4d7d000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001600000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000000007800000000000000000000000000000000000000000000000000000000064d281e65c9438a5a99c4bccb1035296d5d2d8d200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000000320000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb4800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000200000000000000000000000009be264469ef954c139da4a45cf76cbcc5e3a6a73000000000000000000000000000000000000000000000000000000000000271000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000006000000000000000000000000e592427a0aece92de3edee1f18e0157c05861564000000000000000000000000000000000000000000000000000000000000271000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000c0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000064db6806000000000000000000000000000000000000000000000000000000000000002b68037790a0229e9ce6eaa8a99ea92964106c47030001f4a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48000000000000000000000000000000000000000000000000000000000000000000dac17f958d2ee523a2206206994597c13d831ec700000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000200000000000000000000000009be264469ef954c139da4a45cf76cbcc5e3a6a730000000000000000000000000000000000000000000000000000000000002710000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000060000000000000000000000001b81d678ffb9c0263b24a97847620c99d213eb14000000000000000000000000000000000000000000000000000000000000271000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000c0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000064db6806000000000000000000000000000000000000000000000000000000000000002ba0b86991c6218b36c1d19d4a2e9eb0ce3606eb48000064dac17f958d2ee523a2206206994597c13d831ec70000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000","to":"0xdef171fe48cf0115b1d80b88dc8eab59176fee57","gas":648318,"gas_price":"18312000018","value":"0","access_list":[{"address":"0x3f41a1cfd3c8b8d9c162de0f42307a0095a6e5df","storage_keys":[]}],"save":true,"save_if_fails":true,"block_header":{"number":"0x110ace7","hash":"0x0000000000000000000000000000000000000000000000000000000000000000","stateRoot":"0xef53217576746e2df5a5acb6993b629e548592008c22e5eb0c543ab0e597102f","parentHash":"0x0cf8a2db87cf124e1c8fceffd12c325e07fb51736c7dce9d0f945913616cb40a","sha3Uncles":"0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347","transactionsRoot":"0xb29cef267cf8e4b1a629f2aaeff8e3b4faf79195efcb63a08e4823070ee85f21","receiptsRoot":"0x9290b9bda89e8bc6173f17fab6b94ef7ffb1d33770e5d0fc9e21039ef936c777","logsBloom":"0x40330cb14709a3aa3021ae29e85c20249ba3bc0c08bf9c7422cf48124a121120853709b6c20d1261603531d2b8b6810feeb920399c23eb1d8601f14e157921f9ac4b55994f4c3e686a0242ae56ea70ed84fb0b04d6ea1eed11e356cd85609fc3bf310367723a6c1b08453ceecc22d8df13f30504822865610bca1197895e7156a9bfd2756614028c1f5cf5e87bd6a43795c61841abc4d01c6475eae29ad813520b0223401451e9a3fe836ad63e967557cc99030243ad151927d4255e93b7391ed6d29882497108c2044092a24cc68291279b70a7f404ba1139210d5e1c25b40beaf2f48cc341d4c38787169830215105c1f014db5b98ccee22a94d3ba0663c1a","timestamp":"0x64d22deb","difficulty":"0x0","gasLimit":"0x1c9c380","gasUsed":"0x1c9b51a","baseFeePerGas":"0x3d5200956","miner":"0xcda9d71bdfae59b89cee131ed3079f8ac4c77062","extraData":"0xd883010c00846765746888676f312e32302e34856c696e7578","mixHash":"0x9096c8da5df4b9bb771f91a81c3bd954d2a9c39c1bf05502877d057b1f76fb04","nonce":"0x0000000000000000","size":"0x0","totalDifficulty":"0x0","transactions":null,"uncles":null},"state_objects":{"0xdac17f958d2ee523a2206206994597c13d831ec7":{"storage":{"0x0000000000000000000000000000000000000000000000000000000000000000":"0x000000000000000000000000c6cde7c39eb2f0f0095f41570af89efc2c1ea828"}}}}' \
  --compressed
```
{% endcode %}
{% endtab %}

{% tab title="JSON" %}
{% code lineNumbers="true" %}
```json
{
  "network_id": "1",
  "block_number": 17884583,
  "transaction_index": 0,
  "from": "0x3f41a1cfd3c8b8d9c162de0f42307a0095a6e5df",
  "input": "0xa94e78ef000000000000000000000000000000000000000000000000000000000000002000000000000000000000000068037790a0229e9ce6eaa8a99ea92964106c470300000000000000000000000000000000000000000000010f0cf064dd592000000000000000000000000000000000000000000000000000000000000145dc1b2e00000000000000000000000000000000000000000000000000000001477f4d7d000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000001600000000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000000007800000000000000000000000000000000000000000000000000000000064d281e65c9438a5a99c4bccb1035296d5d2d8d200000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000000320000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb4800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000200000000000000000000000009be264469ef954c139da4a45cf76cbcc5e3a6a73000000000000000000000000000000000000000000000000000000000000271000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000080000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000200000000000000000000000000000000000000000000000000000000000000006000000000000000000000000e592427a0aece92de3edee1f18e0157c05861564000000000000000000000000000000000000000000000000000000000000271000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000c0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000064db6806000000000000000000000000000000000000000000000000000000000000002b68037790a0229e9ce6eaa8a99ea92964106c47030001f4a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48000000000000000000000000000000000000000000000000000000000000000000dac17f958d2ee523a2206206994597c13d831ec700000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000060000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000200000000000000000000000009be264469ef954c139da4a45cf76cbcc5e3a6a730000000000000000000000000000000000000000000000000000000000002710000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000060000000000000000000000001b81d678ffb9c0263b24a97847620c99d213eb14000000000000000000000000000000000000000000000000000000000000271000000000000000000000000000000000000000000000000000000000000000a0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000c0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000064db6806000000000000000000000000000000000000000000000000000000000000002ba0b86991c6218b36c1d19d4a2e9eb0ce3606eb48000064dac17f958d2ee523a2206206994597c13d831ec70000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
  "to": "0xdef171fe48cf0115b1d80b88dc8eab59176fee57",
  "gas": 648318,
  "gas_price": "18312000018",
  "value": "0",
  "access_list": [
    {
      "address": "0x3f41a1cfd3c8b8d9c162de0f42307a0095a6e5df",
      "storage_keys": []
    }
  ],
  "save": true,
  "save_if_fails": true,
  "block_header": {
    "number": "0x110ace7",
    "hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "stateRoot": "0xef53217576746e2df5a5acb6993b629e548592008c22e5eb0c543ab0e597102f",
    "parentHash": "0x0cf8a2db87cf124e1c8fceffd12c325e07fb51736c7dce9d0f945913616cb40a",
    "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
    "transactionsRoot": "0xb29cef267cf8e4b1a629f2aaeff8e3b4faf79195efcb63a08e4823070ee85f21",
    "receiptsRoot": "0x9290b9bda89e8bc6173f17fab6b94ef7ffb1d33770e5d0fc9e21039ef936c777",
    "logsBloom": "0x40330cb14709a3aa3021ae29e85c20249ba3bc0c08bf9c7422cf48124a121120853709b6c20d1261603531d2b8b6810feeb920399c23eb1d8601f14e157921f9ac4b55994f4c3e686a0242ae56ea70ed84fb0b04d6ea1eed11e356cd85609fc3bf310367723a6c1b08453ceecc22d8df13f30504822865610bca1197895e7156a9bfd2756614028c1f5cf5e87bd6a43795c61841abc4d01c6475eae29ad813520b0223401451e9a3fe836ad63e967557cc99030243ad151927d4255e93b7391ed6d29882497108c2044092a24cc68291279b70a7f404ba1139210d5e1c25b40beaf2f48cc341d4c38787169830215105c1f014db5b98ccee22a94d3ba0663c1a",
    "timestamp": "0x64d22deb",
    "difficulty": "0x0",
    "gasLimit": "0x1c9c380",
    "gasUsed": "0x1c9b51a",
    "baseFeePerGas": "0x3d5200956",
    "miner": "0xcda9d71bdfae59b89cee131ed3079f8ac4c77062",
    "extraData": "0xd883010c00846765746888676f312e32302e34856c696e7578",
    "mixHash": "0x9096c8da5df4b9bb771f91a81c3bd954d2a9c39c1bf05502877d057b1f76fb04",
    "nonce": "0x0000000000000000",
    "size": "0x0",
    "totalDifficulty": "0x0",
    "transactions": null,
    "uncles": null
  },
  "state_objects": {
    "0xdac17f958d2ee523a2206206994597c13d831ec7": {
      "storage": {
        "0x0000000000000000000000000000000000000000000000000000000000000000": "0x000000000000000000000000c6cde7c39eb2f0f0095f41570af89efc2c1ea828"
      }
    }
  }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Response Payload Example

To learn more about different simulation types, refer to the [Quick, Abi and Full Mode](../simulation-api/simulation-api-quick-and-full-mode.md) page. The bellow example is using full simulation type.

{% tabs %}
{% tab title="Response Explanation" %}
The response will contain:

#### Transaction

This field contains detailed information about a specific blockchain transaction. Key details include the transaction hash, block number, originating and destination addresses, gas details, input data, nonce, and other relevant details of the transaction, like the status, timestamp, and involved contract addresses.

#### Simulation

This section pertains to the simulation of the transaction on a specific blockchain. It offers details like the ID of the simulation, the project and owner IDs, the block number where the transaction was included, gas used, method invoked, the status of the simulation, and some metadata about the block that contains this transaction. It's used to preview the outcome of a transaction before actually committing it to the blockchain, ensuring that the desired result will occur.

#### Contracts

The contracts field provides in-depth data regarding the contract(s) involved in the transaction. This includes the contract's ID, network ID, balance, verification status, associated standards (like ERC20 in the provided example), token-specific data if the contract is a token, compiler version, and even the source code of the contract in some cases. It's a comprehensive look into the contract's details and specifications.

#### Generated Access List

An access list is a feature introduced in [Ethereum's EIP-2930](https://eips.ethereum.org/EIPS/eip-2930), which specifies a list of addresses and storage keys that the transaction will access, enabling certain gas cost optimizations. If present, the `generated_access_list` field would contain such a list generated for the specific transaction, helping in gas optimization and improving the efficiency of the transaction.
{% endtab %}

{% tab title="JSON" %}
{% code lineNumbers="true" %}
```json
{
  "transaction": {
    "hash": "0xd25e7af24f310141e3adc22d11007203a9cf1589aa1b64f75014fb1f06f2548e",
    "block_hash": "",
    "block_number": 17914632,
    "from": "0x0000000000000000000000000000000000000000",
    "gas": 8000000,
    "gas_price": 0,
    "gas_fee_cap": 0,
    "gas_tip_cap": 0,
    "cumulative_gas_used": 0,
    "gas_used": 21693,
    "effective_gas_price": 0,
    "input": "0x06fdde03",
    "nonce": 0,
    "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
    "index": 0,
    "value": "0x",
    "access_list": [],
    "status": true,
    "addresses": [
      "0x0000000000000000000000000000000000000000",
      "0x6b175474e89094c44da98b954eedeac495271d0f"
    ],
    "contract_ids": [
      "eth:1:0x0000000000000000000000000000000000000000",
      "eth:1:0x6b175474e89094c44da98b954eedeac495271d0f"
    ],
    "network_id": "1",
    "timestamp": "2023-08-14T17:38:47Z",
    "function_selector": "",
    "l1_block_number": 0,
    "l1_timestamp": 0,
    "deposit_tx": false,
    "system_tx": false,
    "sig": {
      "v": "0x0",
      "r": "0x0",
      "s": "0x0"
    },
    "transaction_info": {
      "contract_id": "eth:1:0x6b175474e89094c44da98b954eedeac495271d0f",
      "block_number": 17914632,
      "transaction_id": "0xd25e7af24f310141e3adc22d11007203a9cf1589aa1b64f75014fb1f06f2548e",
      "contract_address": "0x6b175474e89094c44da98b954eedeac495271d0f",
      "method": "name",
      "parameters": null,
      "intrinsic_gas": 21064,
      "refund_gas": 0,
      "call_trace": {
        "hash": "0xd25e7af24f310141e3adc22d11007203a9cf1589aa1b64f75014fb1f06f2548e",
        "contract_name": "Dai",
        "function_name": "name",
        "function_pc": 0,
        "function_op": "CALL",
        "absolute_position": 0,
        "caller_pc": 0,
        "caller_op": "CALL",
        "call_type": "CALL",
        "from": "0x0000000000000000000000000000000000000000",
        "from_balance": "11746159154279879089501",
        "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "to_balance": "0",
        "value": "0",
        "block_timestamp": "0001-01-01T00:00:00Z",
        "gas": 7978936,
        "gas_used": 629,
        "intrinsic_gas": 21064,
        "event_references": null,
        "input": "0x06fdde03",
        "nonce_diff": [
          {
            "address": "0x0000000000000000000000000000000000000000",
            "original": "0",
            "dirty": "1"
          }
        ],
        "output": "0x0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000e44616920537461626c65636f696e000000000000000000000000000000000000",
        "decoded_output": [
          {
            "soltype": {
              "name": "",
              "type": "string",
              "storage_location": "default",
              "components": null,
              "offset": 0,
              "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
              "indexed": false,
              "simple_type": {
                "type": "string"
              }
            },
            "value": "Dai Stablecoin"
          }
        ],
        "network_id": "1",
        "calls": null
      },
      "stack_trace": null,
      "logs": null,
      "balance_diff": null,
      "nonce_diff": [
        {
          "address": "0x0000000000000000000000000000000000000000",
          "original": "0",
          "dirty": "1"
        }
      ],
      "state_diff": null,
      "raw_state_diff": null,
      "console_logs": null,
      "asset_changes": null,
      "balance_changes": null,
      "created_at": "2023-08-14T17:38:47Z"
    },
    "method": "",
    "decoded_input": null,
    "call_trace": [
      {
        "call_type": "CALL",
        "from": "0x0000000000000000000000000000000000000000",
        "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "gas": 7978936,
        "gas_used": 629,
        "type": "CALL",
        "input": "0x06fdde03",
        "output": "0x0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000e44616920537461626c65636f696e000000000000000000000000000000000000",
        "fromBalance": "0x027cc2b44cffc6f51d5d"
      }
    ]
  },
  "simulation": {
    "id": "c06319b8-55b8-48eb-935e-3d7f338cb9af",
    "project_id": "1830efff-aa75-481e-b464-cedaf8b90960",
    "owner_id": "7d5e8b1f-8bf8-4eae-a70f-fb7d354b1cc2",
    "network_id": "1",
    "block_number": 17914632,
    "transaction_index": 0,
    "from": "0x0000000000000000000000000000000000000000",
    "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
    "input": "0x06fdde03",
    "gas": 8000000,
    "gas_price": "0",
    "gas_used": 21693,
    "value": "0",
    "method": "name",
    "status": true,
    "access_list": null,
    "queue_origin": "",
    "block_header": {
      "number": "0x1115b08",
      "hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "stateRoot": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "parentHash": "0x83c670e91707242099e6f5315543d581b1d6ef7ffde829f50d1b3af4b7942713",
      "sha3Uncles": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "transactionsRoot": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "receiptsRoot": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
      "timestamp": "0x64da66a7",
      "difficulty": "0x0",
      "gasLimit": "0x1c9c380",
      "gasUsed": "0xc790ea",
      "miner": "0xcda9d71bdfae59b89cee131ed3079f8ac4c77062",
      "extraData": "0x",
      "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "nonce": "0x0000000000000000",
      "baseFeePerGas": "0x1",
      "size": "0x0",
      "totalDifficulty": "0x0",
      "uncles": null,
      "transactions": null
    },
    "deposit_tx": false,
    "system_tx": false,
    "nonce": 0,
    "addresses": [
      "0x0000000000000000000000000000000000000000",
      "0x6b175474e89094c44da98b954eedeac495271d0f"
    ],
    "contract_ids": [
      "eth:1:0x0000000000000000000000000000000000000000",
      "eth:1:0x6b175474e89094c44da98b954eedeac495271d0f"
    ],
    "shared": false,
    "created_at": "2023-08-15T09:29:22.779602208Z"
  },
  "contracts": [
    {
      "id": "eth:1:0x6b175474e89094c44da98b954eedeac495271d0f",
      "contract_id": "eth:1:0x6b175474e89094c44da98b954eedeac495271d0f",
      "balance": "",
      "network_id": "1",
      "public": true,
      "export": false,
      "verified_by": "etherscan",
      "verification_date": null,
      "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
      "contract_name": "Dai",
      "ens_domain": null,
      "type": "contract",
      "standard": "erc20",
      "standards": [
        "erc20"
      ],
      "token_data": {
        "symbol": "dai",
        "name": "Dai",
        "decimals": 18
      },
      "evm_version": "",
      "compiler_version": "v0.5.12+commit.7709ece9",
      "optimizations_used": false,
      "optimization_runs": 200,
      "libraries": null,
      "data": {
        "main_contract": 0,
        "contract_info": [
          {
            "id": 0,
            "path": "Dai.sol",
            "name": "Dai.sol",
            "source": "// hevm: flattened sources of /nix/store/8xb41r4qd0cjb63wcrxf1qmfg88p0961-dss-6fd7de0/src/dai.sol\npragma solidity =0.5.12;\n\n////// /nix/store/8xb41r4qd0cjb63wcrxf1qmfg88p0961-dss-6fd7de0/src/lib.sol\n// This program is free software: you can redistribute it and/or modify\n// it under the terms of the GNU General Public License as published by\n// the Free Software Foundation, either version 3 of the License, or\n// (at your option) any later version.\n\n// This program is distributed in the hope that it will be useful,\n// but WITHOUT ANY WARRANTY; without even the implied warranty of\n// MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the\n// GNU General Public License for more details.\n\n// You should have received a copy of the GNU General Public License\n// along with this program.  If not, see <http://www.gnu.org/licenses/>.\n\n/* pragma solidity 0.5.12; */\n\ncontract LibNote {\n    event LogNote(\n        bytes4   indexed  sig,\n        address  indexed  usr,\n        bytes32  indexed  arg1,\n        bytes32  indexed  arg2,\n        bytes             data\n    ) anonymous;\n\n    modifier note {\n        _;\n        assembly {\n            // log an 'anonymous' event with a constant 6 words of calldata\n            // and four indexed topics: selector, caller, arg1 and arg2\n            let mark := msize                         // end of memory ensures zero\n            mstore(0x40, add(mark, 288))              // update free memory pointer\n            mstore(mark, 0x20)                        // bytes type data offset\n            mstore(add(mark, 0x20), 224)              // bytes size (padded)\n            calldatacopy(add(mark, 0x40), 0, 224)     // bytes payload\n            log4(mark, 288,                           // calldata\n                 shl(224, shr(224, calldataload(0))), // msg.sig\n                 caller,                              // msg.sender\n                 calldataload(4),                     // arg1\n                 calldataload(36)                     // arg2\n                )\n        }\n    }\n}\n\n////// /nix/store/8xb41r4qd0cjb63wcrxf1qmfg88p0961-dss-6fd7de0/src/dai.sol\n// Copyright (C) 2017, 2018, 2019 dbrock, rain, mrchico\n\n// This program is free software: you can redistribute it and/or modify\n// it under the terms of the GNU Affero General Public License as published by\n// the Free Software Foundation, either version 3 of the License, or\n// (at your option) any later version.\n//\n// This program is distributed in the hope that it will be useful,\n// but WITHOUT ANY WARRANTY; without even the implied warranty of\n// MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the\n// GNU Affero General Public License for more details.\n//\n// You should have received a copy of the GNU Affero General Public License\n// along with this program.  If not, see <https://www.gnu.org/licenses/>.\n\n/* pragma solidity 0.5.12; */\n\n/* import \"./lib.sol\"; */\n\ncontract Dai is LibNote {\n    // --- Auth ---\n    mapping (address => uint) public wards;\n    function rely(address guy) external note auth { wards[guy] = 1; }\n    function deny(address guy) external note auth { wards[guy] = 0; }\n    modifier auth {\n        require(wards[msg.sender] == 1, \"Dai/not-authorized\");\n        _;\n    }\n\n    // --- ERC20 Data ---\n    string  public constant name     = \"Dai Stablecoin\";\n    string  public constant symbol   = \"DAI\";\n    string  public constant version  = \"1\";\n    uint8   public constant decimals = 18;\n    uint256 public totalSupply;\n\n    mapping (address => uint)                      public balanceOf;\n    mapping (address => mapping (address => uint)) public allowance;\n    mapping (address => uint)                      public nonces;\n\n    event Approval(address indexed src, address indexed guy, uint wad);\n    event Transfer(address indexed src, address indexed dst, uint wad);\n\n    // --- Math ---\n    function add(uint x, uint y) internal pure returns (uint z) {\n        require((z = x + y) >= x);\n    }\n    function sub(uint x, uint y) internal pure returns (uint z) {\n        require((z = x - y) <= x);\n    }\n\n    // --- EIP712 niceties ---\n    bytes32 public DOMAIN_SEPARATOR;\n    // bytes32 public constant PERMIT_TYPEHASH = keccak256(\"Permit(address holder,address spender,uint256 nonce,uint256 expiry,bool allowed)\");\n    bytes32 public constant PERMIT_TYPEHASH = 0xea2aa0a1be11a07ed86d755c93467f4f82362b452371d1ba94d1715123511acb;\n\n    constructor(uint256 chainId_) public {\n        wards[msg.sender] = 1;\n        DOMAIN_SEPARATOR = keccak256(abi.encode(\n            keccak256(\"EIP712Domain(string name,string version,uint256 chainId,address verifyingContract)\"),\n            keccak256(bytes(name)),\n            keccak256(bytes(version)),\n            chainId_,\n            address(this)\n        ));\n    }\n\n    // --- Token ---\n    function transfer(address dst, uint wad) external returns (bool) {\n        return transferFrom(msg.sender, dst, wad);\n    }\n    function transferFrom(address src, address dst, uint wad)\n        public returns (bool)\n    {\n        require(balanceOf[src] >= wad, \"Dai/insufficient-balance\");\n        if (src != msg.sender && allowance[src][msg.sender] != uint(-1)) {\n            require(allowance[src][msg.sender] >= wad, \"Dai/insufficient-allowance\");\n            allowance[src][msg.sender] = sub(allowance[src][msg.sender], wad);\n        }\n        balanceOf[src] = sub(balanceOf[src], wad);\n        balanceOf[dst] = add(balanceOf[dst], wad);\n        emit Transfer(src, dst, wad);\n        return true;\n    }\n    function mint(address usr, uint wad) external auth {\n        balanceOf[usr] = add(balanceOf[usr], wad);\n        totalSupply    = add(totalSupply, wad);\n        emit Transfer(address(0), usr, wad);\n    }\n    function burn(address usr, uint wad) external {\n        require(balanceOf[usr] >= wad, \"Dai/insufficient-balance\");\n        if (usr != msg.sender && allowance[usr][msg.sender] != uint(-1)) {\n            require(allowance[usr][msg.sender] >= wad, \"Dai/insufficient-allowance\");\n            allowance[usr][msg.sender] = sub(allowance[usr][msg.sender], wad);\n        }\n        balanceOf[usr] = sub(balanceOf[usr], wad);\n        totalSupply    = sub(totalSupply, wad);\n        emit Transfer(usr, address(0), wad);\n    }\n    function approve(address usr, uint wad) external returns (bool) {\n        allowance[msg.sender][usr] = wad;\n        emit Approval(msg.sender, usr, wad);\n        return true;\n    }\n\n    // --- Alias ---\n    function push(address usr, uint wad) external {\n        transferFrom(msg.sender, usr, wad);\n    }\n    function pull(address usr, uint wad) external {\n        transferFrom(usr, msg.sender, wad);\n    }\n    function move(address src, address dst, uint wad) external {\n        transferFrom(src, dst, wad);\n    }\n\n    // --- Approve by signature ---\n    function permit(address holder, address spender, uint256 nonce, uint256 expiry,\n                    bool allowed, uint8 v, bytes32 r, bytes32 s) external\n    {\n        bytes32 digest =\n            keccak256(abi.encodePacked(\n                \"\\x19\\x01\",\n                DOMAIN_SEPARATOR,\n                keccak256(abi.encode(PERMIT_TYPEHASH,\n                                     holder,\n                                     spender,\n                                     nonce,\n                                     expiry,\n                                     allowed))\n        ));\n\n        require(holder != address(0), \"Dai/invalid-address-0\");\n        require(holder == ecrecover(digest, v, r, s), \"Dai/invalid-permit\");\n        require(expiry == 0 || now <= expiry, \"Dai/permit-expired\");\n        require(nonce == nonces[holder]++, \"Dai/invalid-nonce\");\n        uint wad = allowed ? uint(-1) : 0;\n        allowance[holder][spender] = wad;\n        emit Approval(holder, spender, wad);\n    }\n}"
          }
        ],
        "abi": [
          {
            "type": "constructor",
            "name": "",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": [
              {
                "name": "chainId_",
                "type": "uint256",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "uint"
                }
              }
            ],
            "outputs": null
          },
          {
            "type": "function",
            "name": "decimals",
            "constant": true,
            "anonymous": false,
            "stateMutability": "view",
            "inputs": [],
            "outputs": [
              {
                "name": "",
                "type": "uint8",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "uint"
                }
              }
            ]
          }
        ],
        "raw_abi": [
          {
            "inputs": [
              {
                "internalType": "uint256",
                "name": "chainId_",
                "type": "uint256"
              }
            ],
            "payable": false,
            "stateMutability": "nonpayable",
            "type": "constructor"
          },
          {
            "anonymous": false,
            "inputs": [
              {
                "indexed": true,
                "internalType": "address",
                "name": "src",
                "type": "address"
              },
              {
                "indexed": true,
                "internalType": "address",
                "name": "guy",
                "type": "address"
              },
              {
                "indexed": false,
                "internalType": "uint256",
                "name": "wad",
                "type": "uint256"
              }
            ],
            "name": "Approval",
            "type": "event"
          }
        ],
        "states": [
          {
            "name": "nonces",
            "type": "mapping (address => uint256)",
            "storage_location": "storage",
            "components": null,
            "offset": 0,
            "index": "0x0000000000000000000000000000000000000000000000000000000000000004",
            "indexed": false
          },
          {
            "name": "DOMAIN_SEPARATOR",
            "type": "bytes32",
            "storage_location": "storage",
            "components": null,
            "offset": 0,
            "index": "0x0000000000000000000000000000000000000000000000000000000000000005",
            "indexed": false,
            "simple_type": {
              "type": "bytes"
            }
          },
          {
            "name": "wards",
            "type": "mapping (address => uint256)",
            "storage_location": "storage",
            "components": null,
            "offset": 0,
            "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "indexed": false
          },
          {
            "name": "totalSupply",
            "type": "uint256",
            "storage_location": "storage",
            "components": null,
            "offset": 0,
            "index": "0x0000000000000000000000000000000000000000000000000000000000000001",
            "indexed": false,
            "simple_type": {
              "type": "uint"
            }
          },
          {
            "name": "balanceOf",
            "type": "mapping (address => uint256)",
            "storage_location": "storage",
            "components": null,
            "offset": 0,
            "index": "0x0000000000000000000000000000000000000000000000000000000000000002",
            "indexed": false
          },
          {
            "name": "allowance",
            "type": "mapping (address => mapping (address => uint256))",
            "storage_location": "storage",
            "components": null,
            "offset": 0,
            "index": "0x0000000000000000000000000000000000000000000000000000000000000003",
            "indexed": false
          }
        ]
      },
      "creation_block": 0,
      "creation_tx": "",
      "creator_address": "",
      "created_at": "2023-07-27T11:32:46Z",
      "language": "solidity",
      "in_project": false
    }
  ],
  "generated_access_list": []
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Optimism Request Payload

Transaction payload for the Optimism network has additional fields you can use inside the API.

<table><thead><tr><th width="204">Field</th><th width="94">Type</th><th width="185">Description</th><th width="119">Mandatory</th><th>Example Value</th></tr></thead><tbody><tr><td><strong>l1_block_number</strong></td><td>number</td><td>The latest L1 block number known to L2</td><td>No</td><td>100004000</td></tr><tr><td><strong>l1_timestamp</strong></td><td>number</td><td>The timestamp of the latest L1 block</td><td>No</td><td>1686124292</td></tr><tr><td><strong>l1_message_sender</strong></td><td>string</td><td>The address of the sender of the latest message from L1 to L2.</td><td>No</td><td>“0x0000000000000000000000000000000000000000”</td></tr><tr><td><strong>deposit_tx</strong></td><td>boolean</td><td>Indicates if the transaction is a deposit from L1 to L2. It applies for the Bedrock transactions.</td><td>No</td><td>false</td></tr><tr><td><strong>system_tx</strong></td><td>boolean</td><td>Indicates if the transaction is a system-level operation within L2. It applies for the Bedrock transactions.</td><td>No</td><td>false</td></tr><tr><td><strong>mint</strong></td><td>number</td><td>The amount of a specific token minted within L2. It applies for the Bedrock transactions.</td><td>No</td><td>0</td></tr><tr><td><strong>amount_to_mint</strong></td><td>string</td><td>The desired amount to be minted in the next operation. It applies for the Bedrock transactions.</td><td>No</td><td>“0”</td></tr></tbody></table>

### Optimism Request Payload Example

Replace `TENDERLY_ACCOUNT_NAME` and `TENDERLY_PROJECT_NAME` with appropriate values using our [platform access](../../other/platform-access/) guide.

{% tabs %}
{% tab title="fetch" %}
{% code lineNumbers="true" %}
```javascript
await fetch("https://api.tenderly.co/api/v1/account/{{TENDERLY_ACCOUNT_NAME}}/project/{{TENDERLY_PROJECT_NAME}}/simulate", {
  "headers": {
    "authorization": "Bearer <TOKEN>",
    "content-type": "application/json"
  },
  "body": "{\"network_id\":\"10\",\"block_number\":null,\"transaction_index\":null,\"from\":\"0x0000000000000000000000000000000000000000\",\"input\":\"0x8da5cb5b\",\"to\":\"0x11111112542d85b3ef69ae05771c2dccff4faa26\",\"gas\":8000000,\"gas_price\":\"0\",\"value\":\"0\",\"access_list\":[],\"generate_access_list\":true,\"save\":true,\"block_header\":null,\"l1_block_number\":null,\"l1_timestamp\":null,\"l1_message_sender\":\"0x0000000000000000000000000000000000000000\",\"deposit_tx\":false,\"mint\":0,\"amount_to_mint\":\"0\"}",
  "method": "POST"
});
```
{% endcode %}
{% endtab %}

{% tab title="cURL" %}
{% code lineNumbers="true" %}
```bash
curl 'https://api.tenderly.co/api/v1/account/{{TENDERLY_ACCOUNT_NAME}}/project/{{TENDERLY_PROJECT_NAME}}/simulate' \
  -H 'authorization: Bearer <TOKEN>' \
  -H 'content-type: application/json' \
  --data-raw '{"network_id":"10","block_number":null,"transaction_index":null,"from":"0x0000000000000000000000000000000000000000","input":"0x8da5cb5b","to":"0x11111112542d85b3ef69ae05771c2dccff4faa26","gas":8000000,"gas_price":"0","value":"0","access_list":[],"generate_access_list":true,"save":true,"block_header":null,"l1_block_number":null,"l1_timestamp":null,"l1_message_sender":"0x0000000000000000000000000000000000000000","deposit_tx":false,"mint":0,"amount_to_mint":"0"}' \
  --compressed
```
{% endcode %}
{% endtab %}

{% tab title="JSON" %}
{% code lineNumbers="true" %}
```json
{
  "network_id": "10",
  "block_number": null,
  "transaction_index": null,
  "from": "0x0000000000000000000000000000000000000000",
  "input": "0x8da5cb5b",
  "to": "0x11111112542d85b3ef69ae05771c2dccff4faa26",
  "gas": 8000000,
  "gas_price": "0",
  "value": "0",
  "access_list": [],
  "generate_access_list": true,
  "save": true,
  "block_header": null,
  "l1_block_number": null,
  "l1_timestamp": null,
  "l1_message_sender": "0x0000000000000000000000000000000000000000",
  "deposit_tx": false,
  "mint": 0,
  "amount_to_mint": "0"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Optimism Response Payload Example

{% tabs %}
{% tab title="Response Explanation" %}
The response will have the same fields as presented in [#response-payload-example](tenderly-simulation-api.md#response-payload-example "mention").
{% endtab %}

{% tab title="JSON" %}
```json
{
  "transaction": {
    "hash": "0xec0729ed71507155212ea5942ac8a4f0a6e7559c6aa0426353e00b0f751b62f5",
    "block_hash": "",
    "block_number": 108334091,
    "from": "0x0000000000000000000000000000000000000000",
    "gas": 8000000,
    "gas_price": 0,
    "gas_fee_cap": 0,
    "gas_tip_cap": 0,
    "cumulative_gas_used": 0,
    "gas_used": 23432,
    "effective_gas_price": 0,
    "input": "0x8da5cb5b",
    "nonce": 0,
    "to": "0x11111112542d85b3ef69ae05771c2dccff4faa26",
    "index": 0,
    "value": "0x",
    "access_list": [],
    "status": true,
    "addresses": [
      "0x0000000000000000000000000000000000000000",
      "0x11111112542d85b3ef69ae05771c2dccff4faa26"
    ],
    "contract_ids": [
      "eth:10:0x0000000000000000000000000000000000000000",
      "eth:10:0x11111112542d85b3ef69ae05771c2dccff4faa26"
    ],
    "network_id": "10",
    "timestamp": "2023-08-17T10:09:18Z",
    "function_selector": "",
    "l1_message_sender": "0x0000000000000000000000000000000000000000",
    "l1_block_number": 0,
    "l1_timestamp": 0,
    "deposit_tx": false,
    "system_tx": false,
    "mint": 0,
    "sig": {
      "v": "0x0",
      "r": "0x0",
      "s": "0x0"
    },
    "transaction_info": {
      "contract_id": "eth:10:0x11111112542d85b3ef69ae05771c2dccff4faa26",
      "block_number": 108334091,
      "transaction_id": "0xec0729ed71507155212ea5942ac8a4f0a6e7559c6aa0426353e00b0f751b62f5",
      "contract_address": "0x11111112542d85b3ef69ae05771c2dccff4faa26",
      "method": "owner",
      "parameters": null,
      "intrinsic_gas": 21064,
      "refund_gas": 0,
      "call_trace": {
        "hash": "0xec0729ed71507155212ea5942ac8a4f0a6e7559c6aa0426353e00b0f751b62f5",
        "contract_name": "AggregationRouterV3",
        "function_name": "owner",
        "function_pc": 0,
        "function_op": "CALL",
        "absolute_position": 0,
        "caller_pc": 0,
        "caller_op": "CALL",
        "call_type": "CALL",
        "from": "0x0000000000000000000000000000000000000000",
        "from_balance": "479134023710611406",
        "to": "0x11111112542d85b3ef69ae05771c2dccff4faa26",
        "to_balance": "0",
        "value": "0",
        "block_timestamp": "0001-01-01T00:00:00Z",
        "gas": 7978936,
        "gas_used": 2368,
        "intrinsic_gas": 21064,
        "event_references": null,
        "input": "0x8da5cb5b",
        "balance_diff": [
          {
            "address": "0x4200000000000000000000000000000000000019",
            "original": "41411349304876700620",
            "dirty": "41411349304876724052",
            "is_miner": false
          },
          {
            "address": "0x420000000000000000000000000000000000001A",
            "original": "764386804124515085078",
            "dirty": "764386814131493336050",
            "is_miner": false
          }
        ],
        "nonce_diff": [
          {
            "address": "0x0000000000000000000000000000000000000000",
            "original": "0",
            "dirty": "1"
          }
        ],
        "output": "0x0000000000000000000000000000aeb5c94443df71e930727fdce36f74b0d844",
        "decoded_output": [
          {
            "soltype": {
              "name": "",
              "type": "address",
              "storage_location": "default",
              "components": null,
              "offset": 0,
              "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
              "indexed": false,
              "simple_type": {
                "type": "address"
              }
            },
            "value": "0x0000aeb5c94443df71e930727fdce36f74b0d844"
          }
        ],
        "network_id": "10",
        "calls": null
      },
      "stack_trace": null,
      "logs": null,
      "balance_diff": [
        {
          "address": "0x4200000000000000000000000000000000000019",
          "original": "41411349304876700620",
          "dirty": "41411349304876724052",
          "is_miner": false
        },
        {
          "address": "0x420000000000000000000000000000000000001A",
          "original": "764386804124515085078",
          "dirty": "764386814131493336050",
          "is_miner": false
        }
      ],
      "nonce_diff": [
        {
          "address": "0x0000000000000000000000000000000000000000",
          "original": "0",
          "dirty": "1"
        }
      ],
      "state_diff": null,
      "raw_state_diff": null,
      "console_logs": null,
      "asset_changes": null,
      "balance_changes": [],
      "created_at": "2023-08-17T10:09:18Z"
    },
    "method": "",
    "decoded_input": null,
    "call_trace": [
      {
        "call_type": "CALL",
        "from": "0x0000000000000000000000000000000000000000",
        "to": "0x11111112542d85b3ef69ae05771c2dccff4faa26",
        "gas": 7978936,
        "gas_used": 2368,
        "type": "CALL",
        "input": "0x8da5cb5b",
        "output": "0x0000000000000000000000000000aeb5c94443df71e930727fdce36f74b0d844",
        "fromBalance": "0x06a639db231317ce"
      }
    ]
  },
  "simulation": {
    "id": "c9416bba-0b2c-44ae-9abb-fefc6bee9542",
    "project_id": "84d0bc66-5685-407b-93f0-ae298e5fd767",
    "owner_id": "7d5e8b1f-8bf8-4eae-a70f-fb7d354b1cc2",
    "network_id": "10",
    "block_number": 108334091,
    "transaction_index": 0,
    "from": "0x0000000000000000000000000000000000000000",
    "to": "0x11111112542d85b3ef69ae05771c2dccff4faa26",
    "input": "0x8da5cb5b",
    "gas": 8000000,
    "gas_price": "0",
    "gas_used": 23432,
    "value": "0",
    "method": "owner",
    "status": true,
    "access_list": null,
    "l1_message_sender": "0x0000000000000000000000000000000000000000",
    "l1_block_number": 0,
    "l1_timestamp": 1692266958,
    "queue_origin": "",
    "block_header": {
      "number": "0x6750c0b",
      "hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "stateRoot": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "parentHash": "0x8eb650f44182c95fbf388e7e7c997deef4631f5f218507d3c01827b1476e8f83",
      "sha3Uncles": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "transactionsRoot": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "receiptsRoot": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
      "timestamp": "0x64ddf1ce",
      "difficulty": "0x0",
      "gasLimit": "0x1c9c380",
      "gasUsed": "0x4c1cd2",
      "miner": "0x4200000000000000000000000000000000000011",
      "extraData": "0x",
      "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "nonce": "0x0000000000000000",
      "baseFeePerGas": "0x1",
      "size": "0x0",
      "totalDifficulty": "0x0",
      "uncles": null,
      "transactions": null
    },
    "mint": 0,
    "amount_to_mint": "0",
    "deposit_tx": false,
    "system_tx": false,
    "nonce": 0,
    "addresses": [
      "0x0000000000000000000000000000000000000000",
      "0x11111112542d85b3ef69ae05771c2dccff4faa26"
    ],
    "contract_ids": [
      "eth:10:0x0000000000000000000000000000000000000000",
      "eth:10:0x11111112542d85b3ef69ae05771c2dccff4faa26"
    ],
    "shared": false,
    "created_at": "2023-08-17T10:09:19.601271856Z"
  },
  "contracts": [
    {
      "id": "eth:10:0x11111112542d85b3ef69ae05771c2dccff4faa26",
      "contract_id": "eth:10:0x11111112542d85b3ef69ae05771c2dccff4faa26",
      "balance": "",
      "network_id": "10",
      "public": true,
      "export": false,
      "verified_by": "etherscan",
      "verification_date": null,
      "address": "0x11111112542d85b3ef69ae05771c2dccff4faa26",
      "contract_name": "AggregationRouterV3",
      "ens_domain": null,
      "type": "contract",
      "evm_version": "",
      "compiler_version": "v0.7.6+commit.3b061308",
      "optimizations_used": true,
      "optimization_runs": 1000000,
      "libraries": null,
      "data": {
        "main_contract": 0,
        "contract_info": [
          {
            "id": 0,
            "path": "AggregationRouterV3.sol",
            "name": "AggregationRouterV3.sol",
            "source": "/*\r\n                                                           ,▄▓▓██▌   ,╓▄▄▓▓▓▓▓▓▓▓▄▄▄,,                          \r\n                                                        ,▓██▓███▓▄▓███▓╬╬╬╬╬╬╬╬╬╬╬╬╬▓███▓▄,                     \r\n                                                  ▄█   ▓██╬╣███████╬▓▀╬╬▓▓▓████████████▓█████▄,                 \r\n                                                 ▓██▌ ▓██╬╣██████╬▓▌  ██████████████████████▌╙╙▀ⁿ\r\n                                                ▐████████╬▓████▓▓█╨ ▄ ╟█████████▓▓╬╬╬╬╬▓▓█████▓▄\r\n                                  └▀▓▓▄╓        ╟█▓╣█████▓██████▀ ╓█▌ ███████▓▓▓▓▓╬╬╬╬╬╬╬╬╬╬╬╬▓██▓▄\r\n                                     └▀████▓▄╥  ▐██╬╬██████████╙ Æ▀─ ▓███▀╚╠╬╩▀▀███████▓▓╬╬╬╬╬╬╬╬╬██▄\r\n                                        └▀██▓▀▀█████▓╬▓██████▀     ▄█████▒╠\"      └╙▓██████▓╬╬╬╬╬╬╬╬██▄\r\n                                           └▀██▄,└╙▀▀████▌└╙    ^\"▀╙╙╙\"╙██      @▄    ╙▀███████╬╬╬╬╬╬╬██µ\r\n                                              └▀██▓▄, ██▌       ╒       ╙█▓     ]▓█▓╔    ▀███████▓╬╬╬╬╬▓█▌\r\n                                                  ▀█████       ▓         ╟█▌    ]╠██▓░▒╓   ▀████████╬╬╬╬╣█▌\r\n                                                  ▐████      ╓█▀█▌      ,██▌    ╚Å███▓▒▒╠╓  ╙█████████╬╬╬╣█▌\r\n                                                  └████     ▓█░░▓█      ▀▀▀    φ▒╫████▒▒▒▒╠╓  █████████▓╬╬▓█µ\r\n                                                   ╘███µ ▌▄█▓▄▓▀`     ,▀    ,╔╠░▓██████▌╠▒▒▒φ  ██████████╬╬██\r\n                                                   ▐████µ╙▓▀`     ,▀╙,╔╔φφφ╠░▄▓███████▌░▓╙▒▒▒╠ └██╬███████╬▓█⌐\r\n                                                   ╫██ ▓▌         ▌φ▒▒░▓██████████████▌▒░▓╚▒▒▒╠ ▓██╬▓██████╣█▌\r\n                                                   ██▌           ▌╔▒▒▄████████████████▒▒▒░▌╠▒▒▒≥▐██▓╬╬███████▌\r\n                                                   ██▌      ,╓φ╠▓«▒▒▓████▀  ▀█████████▌▒▒▒╟░▒▒▒▒▐███╬╬╣████▓█▌\r\n                                                  ▐██      ╠▒▄▓▓███▓████└     ▀████████▌▒▒░▌╚▒▒▒▐███▓╬╬████ ╙▌\r\n                                                  ███  )  ╠▒░░░▒░╬████▀        └████████░▒▒░╬∩▒▒▓████╬╬╣███\r\n                                                 ▓██    ╠╠▒▒▐█▀▀▌`░╫██           ███████▒▒▒▒░▒▒½█████╬╬╣███\r\n                                                ███ ,█▄ ╠▒▒▒╫▌,▄▀,▒╫██           ╟██████▒▒▒░╣⌠▒▓█████╬╬╣██▌\r\n                                               ╘██µ ██` ╠▒▒░██╬φ╠▄▓██`            ██████░░▌φ╠░▓█████▓╬╬▓██\r\n                                                ╟██  .φ╠▒░▄█▀░░▄██▀└              █████▌▒╣φ▒░▓██████╬╬╣██\r\n                                                 ▀██▄▄▄╓▄███████▀                ▐█████░▓φ▒▄███████▓╬╣██\r\n                                                   ╙▀▀▀██▀└                      ████▓▄▀φ▄▓████████╬▓█▀\r\n                                                                                ▓███╬╩╔╣██████████▓██└\r\n                                                                              ╓████▀▄▓████████▀████▀\r\n                                                                            ,▓███████████████─]██╙\r\n                                                                         ,▄▓██████████████▀└  ╙\r\n                                                                    ,╓▄▓███████████████▀╙\r\n                                                             `\"▀▀▀████████▀▀▀▀`▄███▀▀└\r\n                                                                              └└\r\n                                \r\n                    \r\n\r\n                    11\\   11\\                     11\\             11\\   11\\            11\\                                       11\\       \r\n                  1111 |  \\__|                    11 |            111\\  11 |           11 |                                      11 |      \r\n                  \\_11 |  11\\ 1111111\\   1111111\\ 1111111\\        1111\\ 11 | 111111\\ 111111\\   11\\  11\\  11\\  111111\\   111111\\  11 |  11\\ \r\n                    11 |  11 |11  __11\\ 11  _____|11  __11\\       11 11\\11 |11  __11\\\\_11  _|  11 | 11 | 11 |11  __11\\ 11  __11\\ 11 | 11  |\r\n                    11 |  11 |11 |  11 |11 /      11 |  11 |      11 \\1111 |11111111 | 11 |    11 | 11 | 11 |11 /  11 |11 |  \\__|111111  / \r\n                    11 |  11 |11 |  11 |11 |      11 |  11 |      11 |\\111 |11   ____| 11 |11\\ 11 | 11 | 11 |11 |  11 |11 |      11  _11<  \r\n                  111111\\ 11 |11 |  11 |\\1111111\\ 11 |  11 |      11 | \\11 |\\1111111\\  \\1111  |\\11111\\1111  |\\111111  |11 |      11 | \\11\\ \r\n                  \\______|\\__|\\__|  \\__| \\_______|\\__|  \\__|      \\__|  \\__| \\_______|  \\____/  \\_____\\____/  \\______/ \\__|      \\__|  \\__|\r\n                                                                                                                                           \r\n                                                                                                                                           \r\n                                                                                                                                           \r\n                               111111\\                                                               11\\     11\\                           \r\n                              11  __11\\                                                              11 |    \\__|                          \r\n                              11 /  11 | 111111\\   111111\\   111111\\   111111\\   111111\\   111111\\ 111111\\   11\\  111111\\  1111111\\        \r\n                              11111111 |11  __11\\ 11  __11\\ 11  __11\\ 11  __11\\ 11  __11\\  \\____11\\\\_11  _|  11 |11  __11\\ 11  __11\\       \r\n                              11  __11 |11 /  11 |11 /  11 |11 |  \\__|11111111 |11 /  11 | 1111111 | 11 |    11 |11 /  11 |11 |  11 |      \r\n                              11 |  11 |11 |  11 |11 |  11 |11 |      11   ____|11 |  11 |11  __11 | 11 |11\\ 11 |11 |  11 |11 |  11 |      \r\n                              11 |  11 |\\1111111 |\\1111111 |11 |      \\1111111\\ \\1111111 |\\1111111 | \\1111  |11 |\\111111  |11 |  11 |      \r\n                              \\__|  \\__| \\____11 | \\____11 |\\__|       \\_______| \\____11 | \\_______|  \\____/ \\__| \\______/ \\__|  \\__|      \r\n                                        11\\   11 |11\\   11 |                    11\\   11 |                                                 \r\n                                        \\111111  |\\111111  |                    \\111111  |                                                 \r\n                                         \\______/  \\______/                      \\______/                                                  \r\n                                                1111111\\                        11\\                                                        \r\n                                                11  __11\\                       11 |                                                       \r\n                                                11 |  11 | 111111\\  11\\   11\\ 111111\\    111111\\   111111\\                                 \r\n                                                1111111  |11  __11\\ 11 |  11 |\\_11  _|  11  __11\\ 11  __11\\                                \r\n                                                11  __11< 11 /  11 |11 |  11 |  11 |    11111111 |11 |  \\__|                               \r\n                                                11 |  11 |11 |  11 |11 |  11 |  11 |11\\ 11   ____|11 |                                     \r\n                                                11 |  11 |\\111111  |\\111111  |  \\1111  |\\1111111\\ 11 |                                     \r\n                                                \\__|  \\__| \\______/  \\______/    \\____/  \\_______|\\__|                                     \r\n*/\r\n\r\n// File @openzeppelin/contracts/utils/Context.sol@v3.4.1-solc-0.7-2\r\n\r\n// SPDX-License-Identifier: MIT\r\n\r\npragma solidity >=0.6.0 <0.8.0;\r\n\r\n/*\r\n * @dev Provides information about the current execution context, including the\r\n * sender of the transaction and its data. While these are generally available\r\n * via msg.sender and msg.data, they should not be accessed in such a direct\r\n * manner, since when dealing with GSN meta-transactions the account sending and\r\n * paying for execution may not be the actual sender (as far as an application\r\n * is concerned).\r\n *\r\n * This contract is only required for intermediate, library-like contracts.\r\n */\r\nabstract contract Context {\r\n    function _msgSender() internal view virtual returns (address payable) {\r\n        return msg.sender;\r\n    }\r\n\r\n    function _msgData() internal view virtual returns (bytes memory) {\r\n        this; // silence state mutability warning without generating bytecode - see https://github.com/ethereum/solidity/issues/2691\r\n        return msg.data;\r\n    }\r\n}\r\n\r\n\r\n// File @openzeppelin/contracts/access/Ownable.sol@v3.4.1-solc-0.7-2\r\n\r\n\r\n\r\npragma solidity ^0.7.0;\r\n\r\n/**\r\n * @dev Contract module which provides a basic access control mechanism, where\r\n * there is an account (an owner) that can be granted exclusive access to\r\n * specific functions.\r\n *\r\n * By default, the owner account will be the one that deploys the contract. This\r\n * can later be changed with {transferOwnership}.\r\n *\r\n * This module is used through inheritance. It will make available the modifier\r\n * `onlyOwner`, which can be applied to your functions to restrict their use to\r\n * the owner.\r\n */\r\nabstract contract Ownable is Context {\r\n    address private _owner;\r\n\r\n    event OwnershipTransferred(address indexed previousOwner, address indexed newOwner);\r\n\r\n    /**\r\n     * @dev Initializes the contract setting the deployer as the initial owner.\r\n     */\r\n    constructor () {\r\n        address msgSender = _msgSender();\r\n        _owner = msgSender;\r\n        emit OwnershipTransferred(address(0), msgSender);\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the address of the current owner.\r\n     */\r\n    function owner() public view virtual returns (address) {\r\n        return _owner;\r\n    }\r\n\r\n    /**\r\n     * @dev Throws if called by any account other than the owner.\r\n     */\r\n    modifier onlyOwner() {\r\n        require(owner() == _msgSender(), \"Ownable: caller is not the owner\");\r\n        _;\r\n    }\r\n\r\n    /**\r\n     * @dev Leaves the contract without owner. It will not be possible to call\r\n     * `onlyOwner` functions anymore. Can only be called by the current owner.\r\n     *\r\n     * NOTE: Renouncing ownership will leave the contract without an owner,\r\n     * thereby removing any functionality that is only available to the owner.\r\n     */\r\n    function renounceOwnership() public virtual onlyOwner {\r\n        emit OwnershipTransferred(_owner, address(0));\r\n        _owner = address(0);\r\n    }\r\n\r\n    /**\r\n     * @dev Transfers ownership of the contract to a new account (`newOwner`).\r\n     * Can only be called by the current owner.\r\n     */\r\n    function transferOwnership(address newOwner) public virtual onlyOwner {\r\n        require(newOwner != address(0), \"Ownable: new owner is the zero address\");\r\n        emit OwnershipTransferred(_owner, newOwner);\r\n        _owner = newOwner;\r\n    }\r\n}\r\n\r\n\r\n// File @openzeppelin/contracts/math/SafeMath.sol@v3.4.1-solc-0.7-2\r\n\r\n\r\n\r\npragma solidity ^0.7.0;\r\n\r\n/**\r\n * @dev Wrappers over Solidity's arithmetic operations with added overflow\r\n * checks.\r\n *\r\n * Arithmetic operations in Solidity wrap on overflow. This can easily result\r\n * in bugs, because programmers usually assume that an overflow raises an\r\n * error, which is the standard behavior in high level programming languages.\r\n * `SafeMath` restores this intuition by reverting the transaction when an\r\n * operation overflows.\r\n *\r\n * Using this library instead of the unchecked operations eliminates an entire\r\n * class of bugs, so it's recommended to use it always.\r\n */\r\nlibrary SafeMath {\r\n    /**\r\n     * @dev Returns the addition of two unsigned integers, with an overflow flag.\r\n     *\r\n     * _Available since v3.4._\r\n     */\r\n    function tryAdd(uint256 a, uint256 b) internal pure returns (bool, uint256) {\r\n        uint256 c = a + b;\r\n        if (c < a) return (false, 0);\r\n        return (true, c);\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the substraction of two unsigned integers, with an overflow flag.\r\n     *\r\n     * _Available since v3.4._\r\n     */\r\n    function trySub(uint256 a, uint256 b) internal pure returns (bool, uint256) {\r\n        if (b > a) return (false, 0);\r\n        return (true, a - b);\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the multiplication of two unsigned integers, with an overflow flag.\r\n     *\r\n     * _Available since v3.4._\r\n     */\r\n    function tryMul(uint256 a, uint256 b) internal pure returns (bool, uint256) {\r\n        // Gas optimization: this is cheaper than requiring 'a' not being zero, but the\r\n        // benefit is lost if 'b' is also tested.\r\n        // See: https://github.com/OpenZeppelin/openzeppelin-contracts/pull/522\r\n        if (a == 0) return (true, 0);\r\n        uint256 c = a * b;\r\n        if (c / a != b) return (false, 0);\r\n        return (true, c);\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the division of two unsigned integers, with a division by zero flag.\r\n     *\r\n     * _Available since v3.4._\r\n     */\r\n    function tryDiv(uint256 a, uint256 b) internal pure returns (bool, uint256) {\r\n        if (b == 0) return (false, 0);\r\n        return (true, a / b);\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the remainder of dividing two unsigned integers, with a division by zero flag.\r\n     *\r\n     * _Available since v3.4._\r\n     */\r\n    function tryMod(uint256 a, uint256 b) internal pure returns (bool, uint256) {\r\n        if (b == 0) return (false, 0);\r\n        return (true, a % b);\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the addition of two unsigned integers, reverting on\r\n     * overflow.\r\n     *\r\n     * Counterpart to Solidity's `+` operator.\r\n     *\r\n     * Requirements:\r\n     *\r\n     * - Addition cannot overflow.\r\n     */\r\n    function add(uint256 a, uint256 b) internal pure returns (uint256) {\r\n        uint256 c = a + b;\r\n        require(c >= a, \"SafeMath: addition overflow\");\r\n        return c;\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the subtraction of two unsigned integers, reverting on\r\n     * overflow (when the result is negative).\r\n     *\r\n     * Counterpart to Solidity's `-` operator.\r\n     *\r\n     * Requirements:\r\n     *\r\n     * - Subtraction cannot overflow.\r\n     */\r\n    function sub(uint256 a, uint256 b) internal pure returns (uint256) {\r\n        require(b <= a, \"SafeMath: subtraction overflow\");\r\n        return a - b;\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the multiplication of two unsigned integers, reverting on\r\n     * overflow.\r\n     *\r\n     * Counterpart to Solidity's `*` operator.\r\n     *\r\n     * Requirements:\r\n     *\r\n     * - Multiplication cannot overflow.\r\n     */\r\n    function mul(uint256 a, uint256 b) internal pure returns (uint256) {\r\n        if (a == 0) return 0;\r\n        uint256 c = a * b;\r\n        require(c / a == b, \"SafeMath: multiplication overflow\");\r\n        return c;\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the integer division of two unsigned integers, reverting on\r\n     * division by zero. The result is rounded towards zero.\r\n     *\r\n     * Counterpart to Solidity's `/` operator. Note: this function uses a\r\n     * `revert` opcode (which leaves remaining gas untouched) while Solidity\r\n     * uses an invalid opcode to revert (consuming all remaining gas).\r\n     *\r\n     * Requirements:\r\n     *\r\n     * - The divisor cannot be zero.\r\n     */\r\n    function div(uint256 a, uint256 b) internal pure returns (uint256) {\r\n        require(b > 0, \"SafeMath: division by zero\");\r\n        return a / b;\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the remainder of dividing two unsigned integers. (unsigned integer modulo),\r\n     * reverting when dividing by zero.\r\n     *\r\n     * Counterpart to Solidity's `%` operator. This function uses a `revert`\r\n     * opcode (which leaves remaining gas untouched) while Solidity uses an\r\n     * invalid opcode to revert (consuming all remaining gas).\r\n     *\r\n     * Requirements:\r\n     *\r\n     * - The divisor cannot be zero.\r\n     */\r\n    function mod(uint256 a, uint256 b) internal pure returns (uint256) {\r\n        require(b > 0, \"SafeMath: modulo by zero\");\r\n        return a % b;\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the subtraction of two unsigned integers, reverting with custom message on\r\n     * overflow (when the result is negative).\r\n     *\r\n     * CAUTION: This function is deprecated because it requires allocating memory for the error\r\n     * message unnecessarily. For custom revert reasons use {trySub}.\r\n     *\r\n     * Counterpart to Solidity's `-` operator.\r\n     *\r\n     * Requirements:\r\n     *\r\n     * - Subtraction cannot overflow.\r\n     */\r\n    function sub(uint256 a, uint256 b, string memory errorMessage) internal pure returns (uint256) {\r\n        require(b <= a, errorMessage);\r\n        return a - b;\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the integer division of two unsigned integers, reverting with custom message on\r\n     * division by zero. The result is rounded towards zero.\r\n     *\r\n     * CAUTION: This function is deprecated because it requires allocating memory for the error\r\n     * message unnecessarily. For custom revert reasons use {tryDiv}.\r\n     *\r\n     * Counterpart to Solidity's `/` operator. Note: this function uses a\r\n     * `revert` opcode (which leaves remaining gas untouched) while Solidity\r\n     * uses an invalid opcode to revert (consuming all remaining gas).\r\n     *\r\n     * Requirements:\r\n     *\r\n     * - The divisor cannot be zero.\r\n     */\r\n    function div(uint256 a, uint256 b, string memory errorMessage) internal pure returns (uint256) {\r\n        require(b > 0, errorMessage);\r\n        return a / b;\r\n    }\r\n\r\n    /**\r\n     * @dev Returns the remainder of dividing two unsigned integers. (unsigned integer modulo),\r\n     * reverting with custom message when dividing by zero.\r\n     *\r\n     * CAUTION: This function is deprecated because it requires allocating memory for the error\r\n     * message unnecessarily. For custom revert reasons use {tryMod}.\r\n     *\r\n     * Counterpart to Solidity's `%` operator. This function uses a `revert`\r\n     * opcode (which leaves remaining gas untouched) while Solidity uses an\r\n     * invalid opcode to revert (consuming all remaining gas).\r\n     *\r\n     * Requirements:\r\n     *\r\n     * - The divisor cannot be zero.\r\n     */\r\n    function mod(uint256 a, uint256 b, string memory errorMessage) internal pure returns (uint256) {\r\n        require(b > 0, errorMessage);\r\n        return a % b;\r\n    }\r\n}\r\n\r\n\r\n// File @openzeppelin/contracts/token/ERC20/IERC20.sol@v3.4.1-solc-0.7-2\r\n\r\n\r\n\r\npragma solidity ^0.7.0;\r\n\r\n/**\r\n * @dev Interface of the ERC20 standard as defined in the EIP.\r\n */\r\ninterface IERC20 {\r\n    /**\r\n     * @dev Returns the amount of tokens in existence.\r\n     */\r\n    function totalSupply() external view returns (uint256);\r\n\r\n    /**\r\n     * @dev Returns the amount of tokens owned by `account`.\r\n     */\r\n    function balanceOf(address account) external view returns (uint256);\r\n\r\n    /**\r\n     * @dev Moves `amount` tokens from the caller's account to `recipient`.\r\n     *\r\n     * Returns a boolean value indicating whether the operation succeeded.\r\n     *\r\n     * Emits a {Transfer} event.\r\n     */\r\n    function transfer(address recipient, uint256 amount) external returns (bool);\r\n\r\n    /**\r\n     * @dev Returns the remaining number of tokens that `spender` will be\r\n     * allowed to spend on behalf of `owner` through {transferFrom}. This is\r\n     * zero by default.\r\n     *\r\n     * This value changes when {approve} or {transferFrom} are called.\r\n     */\r\n    function allowance(address owner, address spender) external view returns (uint256);\r\n\r\n    /**\r\n     * @dev Sets `amount` as the allowance of `spender` over the caller's tokens.\r\n     *\r\n     * Returns a boolean value indicating whether the operation succeeded.\r\n     *\r\n     * IMPORTANT: Beware that changing an allowance with this method brings the risk\r\n     * that someone may use both the old and the new allowance by unfortunate\r\n     * transaction ordering. One possible solution to mitigate this race\r\n     * condition is to first reduce the spender's allowance to 0 and set the\r\n     * desired value afterwards:\r\n     * https://github.com/ethereum/EIPs/issues/20#issuecomment-263524729\r\n     *\r\n     * Emits an {Approval} event.\r\n     */\r\n    function approve(address spender, uint256 amount) external returns (bool);\r\n\r\n    /**\r\n     * @dev Moves `amount` tokens from `sender` to `recipient` using the\r\n     * allowance mechanism. `amount` is then deducted from the caller's\r\n     * allowance.\r\n     *\r\n     * Returns a boolean value indicating whether the operation succeeded.\r\n     *\r\n     * Emits a {Transfer} event.\r\n     */\r\n    function transferFrom(address sender, address recipient, uint256 amount) external returns (bool);\r\n\r\n    /**\r\n     * @dev Emitted when `value` tokens are moved from one account (`from`) to\r\n     * another (`to`).\r\n     *\r\n     * Note that `value` may be zero.\r\n     */\r\n    event Transfer(address indexed from, address indexed to, uint256 value);\r\n\r\n    /**\r\n     * @dev Emitted when the allowance of a `spender` for an `owner` is set by\r\n     * a call to {approve}. `value` is the new allowance.\r\n     */\r\n    event Approval(address indexed owner, address indexed spender, uint256 value);\r\n}\r\n\r\n\r\n// File contracts/helpers/UniERC20.sol\r\n\r\n\r\n\r\npragma solidity ^0.7.6;\r\n\r\n\r\nlibrary UniERC20 {\r\n    using SafeMath for uint256;\r\n\r\n    IERC20 private constant _ETH_ADDRESS = IERC20(0xEeeeeEeeeEeEeeEeEeEeeEEEeeeeEeeeeeeeEEeE);\r\n    IERC20 private constant _ZERO_ADDRESS = IERC20(0);\r\n    IERC20 private constant _WETH_ADDRESS = IERC20(0x4200000000000000000000000000000000000006);\r\n\r\n    function isETH(IERC20 token) internal pure returns (bool) {\r\n        return (token == _ZERO_ADDRESS || token == _ETH_ADDRESS || token == _WETH_ADDRESS);\r\n    }\r\n\r\n    function uniBalanceOf(IERC20 token, address account) internal view returns (uint256) {\r\n        if (isETH(token)) {\r\n            return account.balance;\r\n        } else {\r\n            return token.balanceOf(account);\r\n        }\r\n    }\r\n\r\n    function uniTransfer(IERC20 token, address payable to, uint256 amount) internal {\r\n        if (amount > 0) {\r\n            if (isETH(token)) {\r\n                to.transfer(amount);\r\n            } else {\r\n                _callOptionalReturn(token, abi.encodeWithSelector(token.transfer.selector, to, amount));\r\n            }\r\n        }\r\n    }\r\n\r\n    function uniApprove(IERC20 token, address to, uint256 amount) internal {\r\n        require(!isETH(token) || token == _WETH_ADDRESS, \"Approve called on ETH\");\r\n\r\n        // solhint-disable-next-line avoid-low-level-calls\r\n        (bool success, bytes memory returndata) = address(token).call(abi.encodeWithSelector(token.approve.selector, to, amount));\r\n\r\n        if (!success || (returndata.length > 0 && !abi.decode(returndata, (bool)))) {\r\n            _callOptionalReturn(token, abi.encodeWithSelector(token.approve.selector, to, 0));\r\n            _callOptionalReturn(token, abi.encodeWithSelector(token.approve.selector, to, amount));\r\n        }\r\n    }\r\n\r\n    function safeTransfer(IERC20 token, address to, uint256 amount) internal {\r\n        _callOptionalReturn(token, abi.encodeWithSelector(token.transfer.selector, to, amount));\r\n    }\r\n\r\n    function safeTransferFrom(IERC20 token, address from, address to, uint256 amount) internal {\r\n        _callOptionalReturn(token, abi.encodeWithSelector(token.transferFrom.selector, from, to, amount));\r\n    }\r\n\r\n\r\n    function _callOptionalReturn(IERC20 token, bytes memory data) private {\r\n        // solhint-disable-next-line avoid-low-level-calls\r\n        (bool success, bytes memory returndata) = address(token).call(data);\r\n        require(success, \"low-level call failed\");\r\n\r\n        if (returndata.length > 0) { // Return data is optional\r\n            require(abi.decode(returndata, (bool)), \"ERC20 operation did not succeed\");\r\n        }\r\n    }\r\n}\r\n\r\n\r\n// File contracts/helpers/RevertReasonParser.sol\r\n\r\n\r\n\r\npragma solidity ^0.7.6;\r\n\r\n\r\nlibrary RevertReasonParser {\r\n    function parse(bytes memory data, string memory prefix) internal pure returns (string memory) {\r\n        // https://solidity.readthedocs.io/en/latest/control-structures.html#revert\r\n        // We assume that revert reason is abi-encoded as Error(string)\r\n\r\n        // 68 = 4-byte selector 0x08c379a0 + 32 bytes offset + 32 bytes length\r\n        if (data.length >= 68 && data[0] == \"\\x08\" && data[1] == \"\\xc3\" && data[2] == \"\\x79\" && data[3] == \"\\xa0\") {\r\n            string memory reason;\r\n            // solhint-disable no-inline-assembly\r\n            assembly {\r\n                // 68 = 32 bytes data length + 4-byte selector + 32 bytes offset\r\n                reason := add(data, 68)\r\n            }\r\n            /*\r\n                revert reason is padded up to 32 bytes with ABI encoder: Error(string)\r\n                also sometimes there is extra 32 bytes of zeros padded in the end:\r\n                https://github.com/ethereum/solidity/issues/10170\r\n                because of that we can't check for equality and instead check\r\n                that string length + extra 68 bytes is less than overall data length\r\n            */\r\n            require(data.length >= 68 + bytes(reason).length, \"Invalid revert reason\");\r\n            return string(abi.encodePacked(prefix, \"Error(\", reason, \")\"));\r\n        }\r\n        // 36 = 4-byte selector 0x4e487b71 + 32 bytes integer\r\n        else if (data.length == 36 && data[0] == \"\\x4e\" && data[1] == \"\\x48\" && data[2] == \"\\x7b\" && data[3] == \"\\x71\") {\r\n            uint256 code;\r\n            // solhint-disable no-inline-assembly\r\n            assembly {\r\n                // 36 = 32 bytes data length + 4-byte selector\r\n                code := mload(add(data, 36))\r\n            }\r\n            return string(abi.encodePacked(prefix, \"Panic(\", _toHex(code), \")\"));\r\n        }\r\n\r\n        return string(abi.encodePacked(prefix, \"Unknown(\", _toHex(data), \")\"));\r\n    }\r\n\r\n    function _toHex(uint256 value) private pure returns(string memory) {\r\n        return _toHex(abi.encodePacked(value));\r\n    }\r\n\r\n    function _toHex(bytes memory data) private pure returns(string memory) {\r\n        bytes16 alphabet = 0x30313233343536373839616263646566;\r\n        bytes memory str = new bytes(2 + data.length * 2);\r\n        str[0] = \"0\";\r\n        str[1] = \"x\";\r\n        for (uint256 i = 0; i < data.length; i++) {\r\n            str[2 * i + 2] = alphabet[uint8(data[i] >> 4)];\r\n            str[2 * i + 3] = alphabet[uint8(data[i] & 0x0f)];\r\n        }\r\n        return string(str);\r\n    }\r\n}\r\n\r\n\r\n// File contracts/interfaces/IERC20Permit.sol\r\n\r\n\r\n\r\npragma solidity ^0.7.6;\r\n\r\n\r\ninterface IERC20Permit {\r\n    function permit(address owner, address spender, uint256 amount, uint256 deadline, uint8 v, bytes32 r, bytes32 s) external;\r\n}\r\n\r\n\r\n// File contracts/helpers/Permitable.sol\r\n\r\n\r\n\r\npragma solidity ^0.7.6;\r\n\r\n\r\n\r\ncontract Permitable {\r\n    event Error(\r\n        string reason\r\n    );\r\n\r\n    function _permit(IERC20 token, uint256 amount, bytes calldata permit) internal {\r\n        if (permit.length == 32 * 7) {\r\n            // solhint-disable-next-line avoid-low-level-calls\r\n            (bool success, bytes memory result) = address(token).call(abi.encodePacked(IERC20Permit.permit.selector, permit));\r\n            if (!success) {\r\n                string memory reason = RevertReasonParser.parse(result, \"Permit call failed: \");\r\n                if (token.allowance(msg.sender, address(this)) < amount) {\r\n                    revert(reason);\r\n                } else {\r\n                    emit Error(reason);\r\n                }\r\n            }\r\n        }\r\n    }\r\n}\r\n\r\n\r\n// File contracts/interfaces/IChi.sol\r\n\r\n\r\n\r\npragma solidity ^0.7.6;\r\n\r\ninterface IChi is IERC20 {\r\n    function mint(uint256 value) external;\r\n    function free(uint256 value) external returns (uint256 freed);\r\n    function freeFromUpTo(address from, uint256 value) external returns (uint256 freed);\r\n}\r\n\r\n\r\n// File contracts/interfaces/IGasDiscountExtension.sol\r\n\r\n\r\n\r\npragma solidity ^0.7.6;\r\n\r\ninterface IGasDiscountExtension {\r\n    function calculateGas(uint256 gasUsed, uint256 flags, uint256 calldataLength) external view returns (IChi, uint256);\r\n}\r\n\r\n\r\n// File contracts/interfaces/IAggregationExecutor.sol\r\n\r\n\r\n\r\npragma solidity ^0.7.6;\r\n\r\ninterface IAggregationExecutor is IGasDiscountExtension {\r\n    function callBytes(bytes calldata data) external payable;  // 0xd9c45357\r\n}\r\n\r\n\r\n// File contracts/AggregationRouterV3.sol\r\n\r\n\r\n\r\npragma solidity ^0.7.6;\r\npragma experimental ABIEncoderV2;\r\n\r\n\r\n\r\n\r\n\r\ncontract AggregationRouterV3 is Ownable, Permitable {\r\n    using SafeMath for uint256;\r\n    using UniERC20 for IERC20;\r\n\r\n    uint256 private constant _PARTIAL_FILL = 0x01;\r\n    uint256 private constant _REQUIRES_EXTRA_ETH = 0x02;\r\n    uint256 private constant _SHOULD_CLAIM = 0x04;\r\n    uint256 private constant _BURN_FROM_MSG_SENDER = 0x08;\r\n    uint256 private constant _BURN_FROM_TX_ORIGIN = 0x10;\r\n\r\n    struct SwapDescription {\r\n        IERC20 srcToken;\r\n        IERC20 dstToken;\r\n        address srcReceiver;\r\n        address dstReceiver;\r\n        uint256 amount;\r\n        uint256 minReturnAmount;\r\n        uint256 flags;\r\n        bytes permit;\r\n    }\r\n\r\n    event Swapped(\r\n        address sender,\r\n        IERC20 srcToken,\r\n        IERC20 dstToken,\r\n        address dstReceiver,\r\n        uint256 spentAmount,\r\n        uint256 returnAmount\r\n    );\r\n\r\n    function discountedSwap(\r\n        IAggregationExecutor caller,\r\n        SwapDescription calldata desc,\r\n        bytes calldata data\r\n    )\r\n        external\r\n        payable\r\n        returns (uint256 returnAmount, uint256 gasLeft, uint256 chiSpent)\r\n    {\r\n        uint256 initialGas = gasleft();\r\n\r\n        // solhint-disable-next-line avoid-low-level-calls\r\n        (bool success, bytes memory returnData) = address(this).delegatecall(abi.encodeWithSelector(this.swap.selector, caller, desc, data));\r\n        if (success) {\r\n            (returnAmount,) = abi.decode(returnData, (uint256, uint256));\r\n        } else {\r\n            if (msg.value > 0) {\r\n                msg.sender.transfer(msg.value);\r\n            }\r\n            emit Error(RevertReasonParser.parse(returnData, \"Swap failed: \"));\r\n        }\r\n\r\n        (IChi chi, uint256 amount) = caller.calculateGas(initialGas.sub(gasleft()), desc.flags, msg.data.length);\r\n        if (amount > 0) {\r\n            chiSpent = chi.freeFromUpTo(msg.sender, amount);\r\n        }\r\n        gasLeft = gasleft();\r\n    }\r\n\r\n    function swap(\r\n        IAggregationExecutor caller,\r\n        SwapDescription calldata desc,\r\n        bytes calldata data\r\n    )\r\n        external\r\n        payable\r\n        returns (uint256 returnAmount, uint256 gasLeft)\r\n    {\r\n        require(desc.minReturnAmount > 0, \"Min return should not be 0\");\r\n        require(data.length > 0, \"data should be not zero\");\r\n\r\n        uint256 flags = desc.flags;\r\n        IERC20 srcToken = desc.srcToken;\r\n        IERC20 dstToken = desc.dstToken;\r\n\r\n        if (flags & _REQUIRES_EXTRA_ETH != 0) {\r\n            require(msg.value > (srcToken.isETH() ? desc.amount : 0), \"Invalid msg.value\");\r\n        } else {\r\n            require(msg.value == (srcToken.isETH() ? desc.amount : 0), \"Invalid msg.value\");\r\n        }\r\n\r\n        if (flags & _SHOULD_CLAIM != 0) {\r\n            require(!srcToken.isETH(), \"Claim token is ETH\");\r\n            _permit(srcToken, desc.amount, desc.permit);\r\n            srcToken.safeTransferFrom(msg.sender, desc.srcReceiver, desc.amount);\r\n        }\r\n\r\n        address dstReceiver = (desc.dstReceiver == address(0)) ? msg.sender : desc.dstReceiver;\r\n        uint256 initialSrcBalance = (flags & _PARTIAL_FILL != 0) ? srcToken.uniBalanceOf(msg.sender) : 0;\r\n        uint256 initialDstBalance = dstToken.uniBalanceOf(dstReceiver);\r\n\r\n        {\r\n            // solhint-disable-next-line avoid-low-level-calls\r\n            (bool success, bytes memory result) = address(caller).call{value: msg.value}(abi.encodePacked(caller.callBytes.selector, data));\r\n            if (!success) {\r\n                revert(RevertReasonParser.parse(result, \"callBytes failed: \"));\r\n            }\r\n        }\r\n\r\n        uint256 spentAmount = desc.amount;\r\n        returnAmount = dstToken.uniBalanceOf(dstReceiver).sub(initialDstBalance);\r\n\r\n        if (flags & _PARTIAL_FILL != 0) {\r\n            spentAmount = initialSrcBalance.add(desc.amount).sub(srcToken.uniBalanceOf(msg.sender));\r\n            require(returnAmount.mul(desc.amount) >= desc.minReturnAmount.mul(spentAmount), \"Return amount is not enough\");\r\n        } else {\r\n            require(returnAmount >= desc.minReturnAmount, \"Return amount is not enough\");\r\n        }\r\n\r\n        emit Swapped(\r\n            msg.sender,\r\n            srcToken,\r\n            dstToken,\r\n            dstReceiver,\r\n            spentAmount,\r\n            returnAmount\r\n        );\r\n\r\n        gasLeft = gasleft();\r\n    }\r\n\r\n    function rescueFunds(IERC20 token, uint256 amount) external onlyOwner {\r\n        token.uniTransfer(msg.sender, amount);\r\n    }\r\n}"
          }
        ],
        "abi": [
          {
            "type": "constructor",
            "name": "",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": null,
            "outputs": null
          },
          {
            "type": "function",
            "name": "rescueFunds",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": [
              {
                "name": "token",
                "type": "address",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "address"
                }
              },
              {
                "name": "amount",
                "type": "uint256",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "uint"
                }
              }
            ],
            "outputs": []
          },
          {
            "type": "function",
            "name": "swap",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": [
              {
                "name": "caller",
                "type": "address",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "address"
                }
              },
              {
                "name": "desc",
                "type": "tuple",
                "storage_location": "default",
                "components": [
                  {
                    "name": "srcToken",
                    "type": "address",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "address"
                    }
                  },
                  {
                    "name": "dstToken",
                    "type": "address",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "address"
                    }
                  },
                  {
                    "name": "srcReceiver",
                    "type": "address",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "address"
                    }
                  },
                  {
                    "name": "dstReceiver",
                    "type": "address",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "address"
                    }
                  },
                  {
                    "name": "amount",
                    "type": "uint256",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "uint"
                    }
                  },
                  {
                    "name": "minReturnAmount",
                    "type": "uint256",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "uint"
                    }
                  },
                  {
                    "name": "flags",
                    "type": "uint256",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "uint"
                    }
                  },
                  {
                    "name": "permit",
                    "type": "bytes",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "bytes"
                    }
                  }
                ],
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false
              },
              {
                "name": "data",
                "type": "bytes",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "bytes"
                }
              }
            ],
            "outputs": [
              {
                "name": "returnAmount",
                "type": "uint256",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "uint"
                }
              },
              {
                "name": "gasLeft",
                "type": "uint256",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "uint"
                }
              }
            ]
          },
          {
            "type": "function",
            "name": "transferOwnership",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": [
              {
                "name": "newOwner",
                "type": "address",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "address"
                }
              }
            ],
            "outputs": []
          },
          {
            "type": "function",
            "name": "discountedSwap",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": [
              {
                "name": "caller",
                "type": "address",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "address"
                }
              },
              {
                "name": "desc",
                "type": "tuple",
                "storage_location": "default",
                "components": [
                  {
                    "name": "srcToken",
                    "type": "address",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "address"
                    }
                  },
                  {
                    "name": "dstToken",
                    "type": "address",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "address"
                    }
                  },
                  {
                    "name": "srcReceiver",
                    "type": "address",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "address"
                    }
                  },
                  {
                    "name": "dstReceiver",
                    "type": "address",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "address"
                    }
                  },
                  {
                    "name": "amount",
                    "type": "uint256",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "uint"
                    }
                  },
                  {
                    "name": "minReturnAmount",
                    "type": "uint256",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "uint"
                    }
                  },
                  {
                    "name": "flags",
                    "type": "uint256",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "uint"
                    }
                  },
                  {
                    "name": "permit",
                    "type": "bytes",
                    "storage_location": "default",
                    "components": null,
                    "offset": 0,
                    "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                    "indexed": false,
                    "simple_type": {
                      "type": "bytes"
                    }
                  }
                ],
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false
              },
              {
                "name": "data",
                "type": "bytes",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "bytes"
                }
              }
            ],
            "outputs": [
              {
                "name": "returnAmount",
                "type": "uint256",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "uint"
                }
              },
              {
                "name": "gasLeft",
                "type": "uint256",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "uint"
                }
              },
              {
                "name": "chiSpent",
                "type": "uint256",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "uint"
                }
              }
            ]
          },
          {
            "type": "function",
            "name": "owner",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": [],
            "outputs": [
              {
                "name": "",
                "type": "address",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "address"
                }
              }
            ]
          },
          {
            "type": "function",
            "name": "renounceOwnership",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": [],
            "outputs": []
          },
          {
            "type": "event",
            "name": "Swapped",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": [
              {
                "name": "sender",
                "type": "address",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "address"
                }
              },
              {
                "name": "srcToken",
                "type": "address",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "address"
                }
              },
              {
                "name": "dstToken",
                "type": "address",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "address"
                }
              },
              {
                "name": "dstReceiver",
                "type": "address",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "address"
                }
              },
              {
                "name": "spentAmount",
                "type": "uint256",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "uint"
                }
              },
              {
                "name": "returnAmount",
                "type": "uint256",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "uint"
                }
              }
            ],
            "outputs": null
          },
          {
            "type": "event",
            "name": "Error",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": [
              {
                "name": "reason",
                "type": "string",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "string"
                }
              }
            ],
            "outputs": null
          },
          {
            "type": "event",
            "name": "OwnershipTransferred",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": [
              {
                "name": "previousOwner",
                "type": "address",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": true,
                "simple_type": {
                  "type": "address"
                }
              },
              {
                "name": "newOwner",
                "type": "address",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": true,
                "simple_type": {
                  "type": "address"
                }
              }
            ],
            "outputs": null
          }
        ],
        "raw_abi": [
          {
            "anonymous": false,
            "inputs": [
              {
                "indexed": false,
                "internalType": "string",
                "name": "reason",
                "type": "string"
              }
            ],
            "name": "Error",
            "type": "event"
          },
          {
            "anonymous": false,
            "inputs": [
              {
                "indexed": true,
                "internalType": "address",
                "name": "previousOwner",
                "type": "address"
              },
              {
                "indexed": true,
                "internalType": "address",
                "name": "newOwner",
                "type": "address"
              }
            ],
            "name": "OwnershipTransferred",
            "type": "event"
          },
          {
            "anonymous": false,
            "inputs": [
              {
                "indexed": false,
                "internalType": "address",
                "name": "sender",
                "type": "address"
              },
              {
                "indexed": false,
                "internalType": "contract IERC20",
                "name": "srcToken",
                "type": "address"
              },
              {
                "indexed": false,
                "internalType": "contract IERC20",
                "name": "dstToken",
                "type": "address"
              },
              {
                "indexed": false,
                "internalType": "address",
                "name": "dstReceiver",
                "type": "address"
              },
              {
                "indexed": false,
                "internalType": "uint256",
                "name": "spentAmount",
                "type": "uint256"
              },
              {
                "indexed": false,
                "internalType": "uint256",
                "name": "returnAmount",
                "type": "uint256"
              }
            ],
            "name": "Swapped",
            "type": "event"
          },
          {
            "inputs": [
              {
                "internalType": "contract IAggregationExecutor",
                "name": "caller",
                "type": "address"
              },
              {
                "components": [
                  {
                    "internalType": "contract IERC20",
                    "name": "srcToken",
                    "type": "address"
                  },
                  {
                    "internalType": "contract IERC20",
                    "name": "dstToken",
                    "type": "address"
                  },
                  {
                    "internalType": "address",
                    "name": "srcReceiver",
                    "type": "address"
                  },
                  {
                    "internalType": "address",
                    "name": "dstReceiver",
                    "type": "address"
                  },
                  {
                    "internalType": "uint256",
                    "name": "amount",
                    "type": "uint256"
                  },
                  {
                    "internalType": "uint256",
                    "name": "minReturnAmount",
                    "type": "uint256"
                  },
                  {
                    "internalType": "uint256",
                    "name": "flags",
                    "type": "uint256"
                  },
                  {
                    "internalType": "bytes",
                    "name": "permit",
                    "type": "bytes"
                  }
                ],
                "internalType": "struct AggregationRouterV3.SwapDescription",
                "name": "desc",
                "type": "tuple"
              },
              {
                "internalType": "bytes",
                "name": "data",
                "type": "bytes"
              }
            ],
            "name": "discountedSwap",
            "outputs": [
              {
                "internalType": "uint256",
                "name": "returnAmount",
                "type": "uint256"
              },
              {
                "internalType": "uint256",
                "name": "gasLeft",
                "type": "uint256"
              },
              {
                "internalType": "uint256",
                "name": "chiSpent",
                "type": "uint256"
              }
            ],
            "stateMutability": "payable",
            "type": "function"
          },
          {
            "inputs": [],
            "name": "owner",
            "outputs": [
              {
                "internalType": "address",
                "name": "",
                "type": "address"
              }
            ],
            "stateMutability": "view",
            "type": "function"
          },
          {
            "inputs": [],
            "name": "renounceOwnership",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
          },
          {
            "inputs": [
              {
                "internalType": "contract IERC20",
                "name": "token",
                "type": "address"
              },
              {
                "internalType": "uint256",
                "name": "amount",
                "type": "uint256"
              }
            ],
            "name": "rescueFunds",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
          },
          {
            "inputs": [
              {
                "internalType": "contract IAggregationExecutor",
                "name": "caller",
                "type": "address"
              },
              {
                "components": [
                  {
                    "internalType": "contract IERC20",
                    "name": "srcToken",
                    "type": "address"
                  },
                  {
                    "internalType": "contract IERC20",
                    "name": "dstToken",
                    "type": "address"
                  },
                  {
                    "internalType": "address",
                    "name": "srcReceiver",
                    "type": "address"
                  },
                  {
                    "internalType": "address",
                    "name": "dstReceiver",
                    "type": "address"
                  },
                  {
                    "internalType": "uint256",
                    "name": "amount",
                    "type": "uint256"
                  },
                  {
                    "internalType": "uint256",
                    "name": "minReturnAmount",
                    "type": "uint256"
                  },
                  {
                    "internalType": "uint256",
                    "name": "flags",
                    "type": "uint256"
                  },
                  {
                    "internalType": "bytes",
                    "name": "permit",
                    "type": "bytes"
                  }
                ],
                "internalType": "struct AggregationRouterV3.SwapDescription",
                "name": "desc",
                "type": "tuple"
              },
              {
                "internalType": "bytes",
                "name": "data",
                "type": "bytes"
              }
            ],
            "name": "swap",
            "outputs": [
              {
                "internalType": "uint256",
                "name": "returnAmount",
                "type": "uint256"
              },
              {
                "internalType": "uint256",
                "name": "gasLeft",
                "type": "uint256"
              }
            ],
            "stateMutability": "payable",
            "type": "function"
          },
          {
            "inputs": [
              {
                "internalType": "address",
                "name": "newOwner",
                "type": "address"
              }
            ],
            "name": "transferOwnership",
            "outputs": [],
            "stateMutability": "nonpayable",
            "type": "function"
          }
        ],
        "states": [
          {
            "name": "_owner",
            "type": "address",
            "storage_location": "storage",
            "components": null,
            "offset": 0,
            "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "indexed": false,
            "simple_type": {
              "type": "address"
            }
          }
        ]
      },
      "creation_block": 0,
      "creation_tx": "",
      "creator_address": "",
      "created_at": "2021-08-09T18:07:20Z",
      "language": "solidity",
      "in_project": false
    }
  ],
  "generated_access_list": [
    {
      "address": "0x420000000000000000000000000000000000001a"
    },
    {
      "address": "0x4200000000000000000000000000000000000019"
    },
    {
      "address": "0x4200000000000000000000000000000000000015",
      "storage_keys": [
        "0x0000000000000000000000000000000000000000000000000000000000000006",
        "0x0000000000000000000000000000000000000000000000000000000000000001",
        "0x0000000000000000000000000000000000000000000000000000000000000005"
      ]
    }
  ]
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
This page is under construction. More endpoints and examples will be added soon.
{% endhint %}
