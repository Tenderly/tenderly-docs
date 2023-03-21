---
description: >-
  Get started with Simulation RPC to simulate transactions with the Tenderly
  Web3 Gateway node.
---

# Simulation RPC

Simulation RPC allows you to use your Tenderly Web3 Gateway node not only to read data and send transactions to the blockchain, but also to simulate transactions in one place. It's possible to use Simulation RPC for the [networks supported in Web3 Gateway](https://app.gitbook.com/o/-LeLQOwIQG3HndcULLU2/s/-LeLQaB11\_TIOtLg8tIW/\~/changes/372/supported-networks-and-languages). For other cases, use [Simulation API](https://app.gitbook.com/o/-LeLQOwIQG3HndcULLU2/s/-LeLQaB11\_TIOtLg8tIW/\~/changes/372/simulations-and-forks/simulation-api).

Simulation RPC allows you to:

* Simulate an arbitrary transaction.
* Select any historical (or latest) block you wish to simulate on and go back in time.
* Pass a pre-simulation **state override map** so you can bring contracts participating in the simulation in a specific state, even if you wouldn't be able to on an actual network (e.g. Mainnet).

To get started, take a look at the following three examples:

* [Performing a single simulation](simulation-rpc.md#performing-a-single-simulation) using `tenderly_simulateTransaction`
* [Performing a simulation using state overrides](simulation-rpc.md#simulating-with-state-overrides)
* [Simulating a bundle of transactions](simulation-rpc.md#bundle-simulations) that involve minting, approving, and transferring DAI using `tenderly_simulateBundle`.

## Performing a single simulation

In this example, we'll do a quick simulation of `0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2` approving 299 to `0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1`. Check the Response for the **Approve** event.

{% tabs %}
{% tab title="Simulation RPC" %}
```bash
curl https://mainnet.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "tenderly_simulateTransaction",
  "params": [
    {
      "from": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
      "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
      "gas": "0x7a1200",
      "gasPrice": "0x0",
      "value": "0x0",
      "data": "0x095ea7b3000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1000000000000000000000000000000000000000000000000000000000000012b"
    },
    "0xfc497b"
  ]
}'
```
{% endtab %}

{% tab title="Simulation RPC Response" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "blockNumber": "0xfc497b",
    "cumulativeGasUsed": "0x0",
    "gasUsed": "0xb412",
    "logs": [
      {
        "anonymous": false,
        "inputs": [
          {
            "name": "src",
            "type": "address",
            "value": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2"
          },
          {
            "name": "guy",
            "type": "address",
            "value": "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
          },
          {
            "name": "wad",
            "type": "uint256",
            "value": "299"
          }
        ],
        "name": "Approval",
        "raw": {
          "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
          "data": "0x000000000000000000000000000000000000000000000000000000000000012b",
          "topics": [
            "0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925",
            "0x000000000000000000000000e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
            "0x000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
          ]
        }
      }
    ],
    "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000200000000000000000000000000028000000000000000002000000000000000000000010000000000000000004000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000010000000000000000000000000040000000000000000000000000000800000",
    "status": true,
    "trace": [
      {
        "decodedInput": [
          {
            "name": "usr",
            "type": "address",
            "value": "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
          },
          {
            "name": "wad",
            "type": "uint256",
            "value": "299"
          }
        ],
        "decodedOutput": [
          {
            "name": "",
            "type": "bool",
            "value": true
          }
        ],
        "from": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
        "gas": "0x79bdb0",
        "gasUsed": "0x5fc2",
        "input": "0x095ea7b3000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1000000000000000000000000000000000000000000000000000000000000012b",
        "method": "approve",
        "output": "0x0000000000000000000000000000000000000000000000000000000000000001",
        "subtraces": 0,
        "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "traceAddress": [0],
        "type": "CALL",
        "value": "0x0"
      }
    ],
    "type": "0x0"
  }
}
```
{% endtab %}
{% endtabs %}

## Simulating with state overrides

The following example shows a simulation of an arbitrary sender `0xe2e2...e2` calling the `mint` function of the [DAI Mainnet contract (`0x6b17...71d0f`)](https://dashboard.tenderly.co/contract/mainnet/0x6b175474e89094c44da98b954eedeac495271d0f).

In order to mint, the sender of the transaction must be a ward, which this address isn't. To simulate minting, we'll need to do a state override. Prior to running the simulation, the value overrides for the contract's storage slots will be applied to the current state of the contract.

When using Simulation RPC, state overrides are the third argument of the `tenderly_simulateTransaction` RPC call. To specify overrides, provide a map from the contract address to the overrides map. The overrides map takes the [smart contract's storage location](https://docs.soliditylang.org/en/latest/internals/layout\_in\_storage.html#mappings-and-dynamic-arrays) as keys and the value override as value.

For this example, we need to override the following:

```
wards['0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2'] = 1
```

The value override must be supplied to the following storage location:

$$
{keccak_{256} \lparen \underbrace{\tt{0xf2...f2}}_\text{\tt{sender}, 20B}\ .\ \underbrace{\tt{0x00..00}}_\text{\tt{wards} slot, 32B}\rparen}
$$

In our case, this evaluates to `0xedd7d04419e9c48ceb6055956cbb4e2091ae310313a4d1fa7cbcfe7561616e03` and the override map (the third argument) looks as follows:

```json
{
  "0x6b175474e89094c44da98b954eedeac495271d0f": {
    "stateDiff": {
      "0xedd7d04419e9c48ceb6055956cbb4e2091ae310313a4d1fa7cbcfe7561616e03": "0x0000000000000000000000000000000000000000000000000000000000000001"
    }
  }
}
```

Here's the cURL performing the request. Check out the Transfer event in the response.

{% tabs %}
{% tab title="Simulation RPC" %}
```bash
# simulate DAI minting by 0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2
# 0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1 gets the minted DAI
# Simulated on the latest block
curl https://mainnet.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "tenderly_simulateTransaction",
  "params": [
    {
      "from": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
      "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
      "gas": "0x7a1200",
      "data": "0x40c10f19000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f10000000000000000000000000000000000000000000000001bc16d674ec80000"
    },
    "latest",
    {
      "0x6b175474e89094c44da98b954eedeac495271d0f": {
        "stateDiff": {
          "0xedd7d04419e9c48ceb6055956cbb4e2091ae310313a4d1fa7cbcfe7561616e03": "0x0000000000000000000000000000000000000000000000000000000000000001"
        }
      }
    }
  ]
}'
```
{% endtab %}

{% tab title="Simulation RPC Response" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "blockNumber": "0xfd0dc8",
    "cumulativeGasUsed": "0x0",
    "gasUsed": "0xd0e5",
    "logs": [
      {
        "anonymous": false,
        "inputs": [
          {
            "name": "src",
            "type": "address",
            "value": "0x0000000000000000000000000000000000000000"
          },
          {
            "name": "dst",
            "type": "address",
            "value": "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
          },
          {
            "name": "wad",
            "type": "uint256",
            "value": "2000000000000000000"
          }
        ],
        "name": "Transfer",
        "raw": {
          "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
          "data": "0x0000000000000000000000000000000000000000000000001bc16d674ec80000",
          "topics": [
            "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
            "0x0000000000000000000000000000000000000000000000000000000000000000",
            "0x000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
          ]
        }
      }
    ],
    "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000010000000020000000004000000000800000000000000000000000010000000000000000000000100000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000002000000000000000000000020000000000000000000000000000000040000000000000000000000000000000000",
    "status": true,
    "trace": [
      {
        "decodedInput": [
          {
            "name": "usr",
            "type": "address",
            "value": "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
          },
          {
            "name": "wad",
            "type": "uint256",
            "value": "2000000000000000000"
          }
        ],
        "from": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
        "gas": "0x79bd80",
        "gasUsed": "0x7c65",
        "input": "0x40c10f19000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f10000000000000000000000000000000000000000000000001bc16d674ec80000",
        "method": "mint",
        "output": "0x",
        "subtraces": 0,
        "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "traceAddress": [0],
        "type": "CALL",
        "value": "0x0"
      }
    ],
    "type": "0x0"
  }
}
```
{% endtab %}
{% endtabs %}

## Simulating a bundle of transactions

The custom `tenderly_simulateBundle` endpoint allows you to simulate several transactions by passing them as an array. The transactions are simulated as if they executed one after another in the same block.

The following code performs a simulation bundle of the following transactions:

1. Minting 2 DAI for `e58b9ee93700a616b50509c8292977fa7a0f8ce1` (if you don't have any already). To achieve this, simulate a call to the **mint** function with a state override to the `wards` mapping, so the address `0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2` becomes a ward for this simulation.
2. Now that `e58b9ee93700a616b50509c8292977fa7a0f8ce1` has 2 DAI, we need a transaction that approves 1 DAI to `f7ddedc66b1d482e5c38e4730b3357d32411e5dd`.
3. A transaction where `0xf7ddedc66b1d482e5c38e4730b3357d32411e5dd` calls `transferFrom` and sends to `e58b9ee93700a616b50509c8292977fa7a0f8ce1`.

Look for the Transfer, Approve, and Transfer events in the response, meaning the effects of prior transactions are visible to subsequent ones.

{% tabs %}
{% tab title="Simulation Bundle RPC" %}
```bash
curl https://mainnet.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "tenderly_simulateBundle",
  "params": [
    [
      {
        "from": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
        "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "data": "0x40c10f19000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce10000000000000000000000000000000000000000000000001bc16d674ec80000"
      },
      {
        "from": "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1",
        "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "gas": "0x7a1200",
        "data": "0x095ea7b3000000000000000000000000f7ddedc66b1d482e5c38e4730b3357d32411e5dd0000000000000000000000000000000000000000000000000de0b6b3a7640000"
      },
      {
        "from": "0xf7ddedc66b1d482e5c38e4730b3357d32411e5dd",
        "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "gas": "0x7a1200",
        "data": "0x23b872dd000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce1000000000000000000000000bd8daa414fda8a8a129f7035e7496759c5af8570000000000000000000000000000000000000000000000000006a94d74f430000"
      }
    ],
    "latest",
    {
      "0x6b175474e89094c44da98b954eedeac495271d0f": {
        "stateDiff": {
          "0xedd7d04419e9c48ceb6055956cbb4e2091ae310313a4d1fa7cbcfe7561616e03": "0x0000000000000000000000000000000000000000000000000000000000000001"
        }
      }
    }
  ]
}'
```
{% endtab %}

{% tab title="Simulation Bundle RPC Response" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": [
    {
      "blockNumber": "0xfd2eff",
      "cumulativeGasUsed": "0x0",
      "gasUsed": "0xd0d9",
      "logs": [
        {
          "anonymous": false,
          "inputs": [
            {
              "name": "src",
              "type": "address",
              "value": "0x0000000000000000000000000000000000000000"
            },
            {
              "name": "dst",
              "type": "address",
              "value": "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1"
            },
            {
              "name": "wad",
              "type": "uint256",
              "value": "2000000000000000000"
            }
          ],
          "name": "Transfer",
          "raw": {
            "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "data": "0x0000000000000000000000000000000000000000000000001bc16d674ec80000",
            "topics": [
              "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
              "0x0000000000000000000000000000000000000000000000000000000000000000",
              "0x000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce1"
            ]
          }
        }
      ],
      "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000010000000020000000000000000000800000000000000000000000010000000000000000000004000800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000002000000000000000000020000000002000000000000000000000020000000000000000000000000000000000000000000000000000000000000000000",
      "status": true,
      "trace": [
        {
          "decodedInput": [
            {
              "name": "usr",
              "type": "address",
              "value": "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1"
            },
            {
              "name": "wad",
              "type": "uint256",
              "value": "2000000000000000000"
            }
          ],
          "from": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
          "gas": "0x5f58c8c",
          "gasUsed": "0x7c65",
          "input": "0x40c10f19000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce10000000000000000000000000000000000000000000000001bc16d674ec80000",
          "method": "mint",
          "output": "0x",
          "subtraces": 0,
          "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
          "traceAddress": [0],
          "type": "CALL",
          "value": "0x0"
        }
      ],
      "type": "0x0"
    },
    {
      "blockNumber": "0xfd2eff",
      "cumulativeGasUsed": "0x0",
      "gasUsed": "0xb442",
      "logs": [
        {
          "anonymous": false,
          "inputs": [
            {
              "name": "src",
              "type": "address",
              "value": "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1"
            },
            {
              "name": "guy",
              "type": "address",
              "value": "0xf7ddedc66b1d482e5c38e4730b3357d32411e5dd"
            },
            {
              "name": "wad",
              "type": "uint256",
              "value": "1000000000000000000"
            }
          ],
          "name": "Approval",
          "raw": {
            "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "data": "0x0000000000000000000000000000000000000000000000000de0b6b3a7640000",
            "topics": [
              "0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925",
              "0x000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce1",
              "0x000000000000000000000000f7ddedc66b1d482e5c38e4730b3357d32411e5dd"
            ]
          }
        }
      ],
      "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000000200000000000000000000000000008000000000000000000000000000000000000000010000000000000000000020000000000000000000000000000000000000000000000000000004000800000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000000000000000000000000000020000000002000000000000000000000000100010000000000000000000000000000000000000000000000000000000000000",
      "status": true,
      "trace": [
        {
          "decodedInput": [
            {
              "name": "usr",
              "type": "address",
              "value": "0xf7ddedc66b1d482e5c38e4730b3357d32411e5dd"
            },
            {
              "name": "wad",
              "type": "uint256",
              "value": "1000000000000000000"
            }
          ],
          "decodedOutput": [
            {
              "name": "",
              "type": "bool",
              "value": true
            }
          ],
          "from": "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1",
          "gas": "0x79bd80",
          "gasUsed": "0x5fc2",
          "input": "0x095ea7b3000000000000000000000000f7ddedc66b1d482e5c38e4730b3357d32411e5dd0000000000000000000000000000000000000000000000000de0b6b3a7640000",
          "method": "approve",
          "output": "0x0000000000000000000000000000000000000000000000000000000000000001",
          "subtraces": 0,
          "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
          "traceAddress": [0],
          "type": "CALL",
          "value": "0x0"
        }
      ],
      "type": "0x0"
    },
    {
      "blockNumber": "0xfd2eff",
      "cumulativeGasUsed": "0x0",
      "gasUsed": "0xe38b",
      "logs": [
        {
          "anonymous": false,
          "inputs": [
            {
              "name": "src",
              "type": "address",
              "value": "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1"
            },
            {
              "name": "dst",
              "type": "address",
              "value": "0xbd8daa414fda8a8a129f7035e7496759c5af8570"
            },
            {
              "name": "wad",
              "type": "uint256",
              "value": "30000000000000000"
            }
          ],
          "name": "Transfer",
          "raw": {
            "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "data": "0x000000000000000000000000000000000000000000000000006a94d74f430000",
            "topics": [
              "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
              "0x000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce1",
              "0x000000000000000000000000bd8daa414fda8a8a129f7035e7496759c5af8570"
            ]
          }
        }
      ],
      "logsBloom": "0x00000000000000800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000010000000000000000000004000800000000000000000000000000000000000000000000000000000000000000000000000000000000000000000040000000000000000000000000002000000000000000000020000000002000000000000000000000000000000000000000000000000004000000000000000000000000000000000000000",
      "status": true,
      "trace": [
        {
          "decodedInput": [
            {
              "name": "src",
              "type": "address",
              "value": "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1"
            },
            {
              "name": "dst",
              "type": "address",
              "value": "0xbd8daa414fda8a8a129f7035e7496759c5af8570"
            },
            {
              "name": "wad",
              "type": "uint256",
              "value": "30000000000000000"
            }
          ],
          "decodedOutput": [
            {
              "name": "",
              "type": "bool",
              "value": true
            }
          ],
          "from": "0xf7ddedc66b1d482e5c38e4730b3357d32411e5dd",
          "gas": "0x79bc28",
          "gasUsed": "0x8db3",
          "input": "0x23b872dd000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce1000000000000000000000000bd8daa414fda8a8a129f7035e7496759c5af8570000000000000000000000000000000000000000000000000006a94d74f430000",
          "method": "transferFrom",
          "output": "0x0000000000000000000000000000000000000000000000000000000000000001",
          "subtraces": 0,
          "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
          "traceAddress": [0],
          "type": "CALL",
          "value": "0x0"
        }
      ],
      "type": "0x0"
    }
  ]
}
```
{% endtab %}
{% endtabs %}
