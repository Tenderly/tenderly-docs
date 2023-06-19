---
description: Explore the list of available custom RPC methods available within DevNets.
---

# Custom RPC Methods

DevNets allow you to easily manipulate the state of the networks to fit your project’s specific needs. Below is a list of custom RPC methods that you can use within DevNets to manipulate the state of the networks, along with usage examples.

### **`evm_increaseTime`**

Jumps forward in time and generates a block with that timestamp.

**Parameters**

* `QUANTITY` - integer or hex-encoded number of seconds to jump forward by

**Returns**

* `DATA` - 32-byte block hash of the newly generated block

**Example request**

```jsx
{
    "jsonrpc": "2.0",
    "method": "evm_increaseTime",
    "params": ["0x15180"],
    "id": "1234"
}
```

**Example response**

```jsx
{
    "jsonrpc": "2.0",
    "result": "0x51e0a03f19e0c154b16363086aa6bbf22ad4582b0515b0a3a00519015f06246f",
    "id": "1234"
}
```

### `evm_setNextBlockTimestamp`

This method works like `evm_increaseTime` but instead of increasing time for specific amount of seconds, it sets the timestamp in the future.

**Parameters**

* `QUANTITY` - integer or hex-encoded number that represents epoch timestamp (in seconds)

**Returns**

* `QUANTITY` - integer (epoch timestamp) that is set for the next block

**Example request**

```jsx
{
	"jsonrpc": "2.0",
	"method": "evm_setNextBlockTimestamp",
	"params": [ "1750074671" ],    # 2025-07-16 11:51:11
	"id": "1234"
}
```

**Example response**

```javascript
{
    "jsonrpc": "2.0",
    "result": 1750074671,
    "id": "1234"
}
```

### `evm_increaseBlocks`

Skips a number of blocks and generates a new block with the new block number.

**Parameters**

* `QUANTITY` - integer or hex-encoded number of blocks to skip

**Returns**

* `DATA` - 32-byte block hash of the newly generated block

**Example request**

```jsx
{
    "jsonrpc": "2.0",
    "method": "evm_increaseBlocks",
    "params": ["0x20"],
    "id": "1234"
}
```

**Example response**

```jsx
{
    "jsonrpc": "2.0",
    "result": "0x51e0a03f19e0c154b16363086aa6bbf22ad4582b0515b0a3a00519015f06246f",
    "id": "1234"
}
```

### `eth_createAccessList`

Returns the access tuples that would be touched by the transaction.

**Parameters**

* `SendTransactionObject` - transaction object (same as the one provided to eth\_sendTransaction)
* `BlockNumber` - block number parameter

**Returns**

* `AccessList` - an array of access tuples touched by the transaction

**Example request**

```jsx
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

**Example response**

```jsx
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

### `evm_getLatest`

Fetches the latest transaction ID on a network fork.

**Parameters**

**Returns**

* `DATA` - UUID of the latest fork transaction

**Example request**

```jsx
{
    "jsonrpc": "2.0",
    "method": "evm_getLatest",
    "params": [],
    "id": "1234"
}
```

**Example response**

```jsx
{
    "jsonrpc": "2.0",
    "result": "4a05d7ed-f66c-471a-899d-d6d843b8e790",
    "id": "1234"
}
```

### `tenderly_setBalance`

Modifies the balance of an account or accounts.

**Parameters**

* `ADDRESS/ADDRESSES` - a string or an array of account addresses
* `AMOUNT` - hex-encoded number of an amount in Wei

**Returns**

* `DATA` - 32-byte block hash of the newly created transaction

**Example request**

```jsx
{
    "jsonrpc": "2.0",
    "method": "tenderly_setBalance",
    "params": [
			["0x0d2026b3EE6eC71FC6746ADb6311F6d3Ba1C000B"],
		  "0xDE0B6B3A7640000",
		],
    "id": "1234"
}
```

OR

```jsx
{
    "jsonrpc": "2.0",
    "method": "tenderly_setBalance",
    "params": [
			"0x0d2026b3EE6eC71FC6746ADb6311F6d3Ba1C000B",
		  "0xDE0B6B3A7640000",
		],
    "id": "1234"
}
```

**Example response**

```jsx
{
    "jsonrpc": "2.0",
    "result": "0xc5b2c658f5fa236c598a6e7fbf7f21413dc42e2a41dd982eb772b30707cba2eb",
    "id": "1234"
}
```

### `tenderly_addBalance`

Adds the balance to the provided account or accounts.

**Parameters**

* `ADDRESS/ADDRESSES` - a string or an array of account addresses
* `AMOUNT` - hex-encoded number of an amount in Wei

**Returns**

* `DATA` - 32-byte block hash of the newly created transaction

**Example request**

```jsx
{
    "jsonrpc": "2.0",
    "method": "tenderly_addBalance",
    "params": [
			["0x0d2026b3EE6eC71FC6746ADb6311F6d3Ba1C000B"],
		  "0xDE0B6B3A7640000",
		],
    "id": "1234"
}
```

OR

```jsx
{
    "jsonrpc": "2.0",
    "method": "tenderly_addBalance",
    "params": [
			"0x0d2026b3EE6eC71FC6746ADb6311F6d3Ba1C000B",
		  "0xDE0B6B3A7640000",
		],
    "id": "1234"
}
```

**Example response**

```jsx
{
    "jsonrpc": "2.0",
    "result": "0xc5b2c658f5fa236c598a6e7fbf7f21413dc42e2a41dd982eb772b30707cba2eb",
    "id": "1234"
}
```

### `tenderly_setStorageAt`

Sets the storage of the provided address at the provided slot.

**Parameters**

* `ADDRESS` - the address where the storage will be overridden
* `SLOT` - 32-byte hash representing the storage slot key
* `VALUE` - 32-byte hash representing the value at the key `slot`

**Returns**

* `DATA` - 32-byte hash of the newly created transaction (storage override is committed via transaction)

**Example request**

```solidity
{
	"jsonrpc":"2.0",
	"method":"tenderly_setStorageAt",
	"params":[
		"0x3Df2f692132f55b97cc9DA04A1fFFEA82F5d710b", //address
		"0x8111de210bcfef10861a4ab6df0f4838296bd61d5a8f02dca283ed3b72a47bba", //slot
		"0x0000000000000000000000000000000000000000000000000000000000000000", //value
	],
	"id":"1"
}
```

**Example response**

```jsx
{
    "jsonrpc": "2.0",
    "result": "0xc5b2c658f5fa236c598a6e7fbf7f21413dc42e2a41dd982eb772b30707cba2eb",
    "id": "1234"
}
```

### `evm_snapshot`

Returns a snapshot ID that allows you to revert a fork to a previous point (same as ID from `getLatest` or the header returned in every RPC request)

**Parameters**

**Returns**

1. `DATA` - UUID of the latest fork transaction

**Example request**

```jsx
{
    "jsonrpc": "2.0",
    "method": "evm_snapshot",
    "params": [],
    "id": "1234"
}
```

**Example response**

```jsx
{
    "jsonrpc": "2.0",
    "result": "4a05d7ed-f66c-471a-899d-d6d843b8e790",
    "id": "1234"
}
```

### `evm_revert`

Reverts the state of the fork to a previous snapshot.

**Parameters**

* `DATA` - UUID of a snapshot (use `0x1` to revert the fork back to the initial state)

**Returns**

* `BOOLEAN` - operation success flag

**Example request**

```jsx
{
    "jsonrpc": "2.0",
    "method": "evm_revert",
    "params": ["0x1"],
    "id": "1234"
}
```

**Example response**

```javascript
{
    "jsonrpc": "2.0",
    "result": true,
    "id": "1234"
}
```
