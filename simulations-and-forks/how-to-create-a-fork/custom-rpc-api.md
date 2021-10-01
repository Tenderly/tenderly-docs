# Custom RPC API

{% hint style="info" %}
All requests to the RPC API will return a new Head header that is used to chain transactions together.
{% endhint %}

## **evm\_increaseTime**

Jump forward in time and generate a block with that timestamp.

#### Parameters

1. `QUANTITY` - integer or hex encoded number of seconds to jump forward by

#### Returns

1. `DATA` - 32 byte block hash of the newly generated block

#### Example:

Request:

```text
{
    "jsonrpc": "2.0",
    "method": "evm_increaseTime",
    "params": ["0x15180"],
    "id": "1234"
}
```

Response:

```text
{
    "jsonrpc": "2.0",
    "result": "0x51e0a03f19e0c154b16363086aa6bbf22ad4582b0515b0a3a00519015f06246f",
    "id": "1234"
}
```

## **evm\_increaseBlocks**

Skip a number of blocks and generate a new block with the new block number.

#### Parameters

1. `QUANTITY` - integer or hex encoded number of blocks to skip

#### Returns

1. `DATA` - 32 byte block hash of the newly generated block

#### Example:

Request:

```text
{
    "jsonrpc": "2.0",
    "method": "evm_increaseBlocks",
    "params": ["0x20"],
    "id": "1234"
}
```

Response:

```text
{
    "jsonrpc": "2.0",
    "result": "0x51e0a03f19e0c154b16363086aa6bbf22ad4582b0515b0a3a00519015f06246f",
    "id": "1234"
}
```

## **eth\_createAccessList**

Return the access tuples that would be touched by the transaction.

#### Parameters

1. `SendTransactionObject` - transaction object \(same as the one provided to eth\_sendTransaction\)
2. `BlockNumber` - block number param

* Example request

  ```text
  {
      "jsonrpc": "2.0",
      "method": "eth_getAccessList",
      "params": [
          {
              "from": "0x7ed8dff35e6fef1a6c1f95423cd8a64e22687aac",
              "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
              "gas": "0x76c00",
              "gasPrice": "0x0",
              "value": "0x0",
              "data": "0xa9059cbb0000000000000000000000005eddecc908575e1adcf857d8be380b9b7e5f658300000000000000000000000000000000000000000000000228813d891ab86000"
          },
          "latest"
      ],
      "id": "1234"
  }
  ```

#### Returns

1. `AccessList` - an array of access tuples touched by the transaction

* Example response

  ```text
  {
      "jsonrpc": "2.0",
      "result": [
          {
              "address": "0x7ed8dff35e6fef1a6c1f95423cd8a64e22687aac"
          },
          {
              "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
              "storage_keys": [
                  "0x5051a693fd89be4fee1466db5a0684c1868dc09405da86e3d13004a803e302ec"
              ]
          },
          {
              "address": "0xc8f595e2084db484f8a80109101d58625223b7c9"
          }
      ],
      "id": 1234
  }
  ```

## **evm\_getLatest**

Fetches the latest transaction id in a fork.

#### Parameters

#### Returns

1. `DATA` - UUID of the latest fork transaction

#### Example:

Request

```text
{
    "jsonrpc": "2.0",
    "method": "evm_getLatest",
    "params": [],
    "id": "1234"
}
```

Response:

```text
{
    "jsonrpc": "2.0",
    "result": "4a05d7ed-f66c-471a-899d-d6d843b8e790",
    "id": "1234"
}
```

