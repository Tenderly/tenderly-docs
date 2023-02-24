---
description: >-
  Learn how to introduce Simulation API into your project by running a single
  simulation using a code example.
---

# Using Simulation API

To get started with Simulation API, follow the code example below. It shows how to use Simulation API to simulate an ERC-20 approval to spend 290 DAI to address `0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1`.&#x20;

The simulation output shows the emitted events and state changes that this transaction might cause if you sent it to the blockchain.

{% hint style="info" %}
You can specify any sender address via the `from` field. Tenderly simulates unsigned transactions, so you don't necessarily need to own an account's private key to simulate transactions from the specified sender.
{% endhint %}

{% tabs %}
{% tab title="Request" %}
```typescript
import axios from 'axios';
import * as dotenv from 'dotenv';
dotenv.config();

const approveDai = async () => {
  // assuming environment variables TENDERLY_USER, TENDERLY_PROJECT and TENDERLY_ACCESS_KEY are set
  // https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name
  // https://docs.tenderly.co/other/platform-access/how-to-generate-api-access-tokens
  const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;

  console.time('Simulation');

  const resp = await axios.post(
    `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/simulate`,
    // the transaction
    {
      /* Simulation Configuration */
      save: false, // if true simulation is saved and shows up in the dashboard
      save_if_fails: false, // if true, reverting simulations show up in the dashboard
      simulation_type: 'full', // full or quick (full is default)

      network_id: '1', // network to simulate on

      /* Standard EVM Transaction object */
      from: '0xdc6bdc37b2714ee601734cf55a05625c9e512461',
      to: '0x6b175474e89094c44da98b954eedeac495271d0f',
      input:
        '0x095ea7b3000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1000000000000000000000000000000000000000000000000000000000000012b',
      gas: 8000000,
      gas_price: 0,
      value: 0,
    },
    {
      headers: {
        'X-Access-Key': TENDERLY_ACCESS_KEY as string,
      },
    }
  );
  console.timeEnd('Simulation');

  const transcation = resp.data.transaction;
  console.log(JSON.stringify(transcation, null, 2));

};

approveDai();

```
{% endtab %}

{% tab title="Result" %}
```txt
Simulation: 180.699ms
{
  "hash": "0x1e44c2d964c9805b235475e55c31c27785aa2fc00129d2a4b21ed5eed6928929",
  "block_hash": "",
  "block_number": 16598287,
  "from": "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
  "gas": 8000000,
  "gas_price": 0,
  "gas_fee_cap": 0,
  "gas_tip_cap": 0,
  "cumulative_gas_used": 0,
  "gas_used": 46098,
  "effective_gas_price": 0,
  "input": "0x095ea7b3000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1000000000000000000000000000000000000000000000000000000000000012b",
  "nonce": 0,
  "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
  "index": 0,
  "value": "0x",
  "access_list": null,
  "status": true,
  "addresses": [
    "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
    "0x6b175474e89094c44da98b954eedeac495271d0f"
  ],
  "contract_ids": [
    "eth:1:0xdc6bdc37b2714ee601734cf55a05625c9e512461",
    "eth:1:0x6b175474e89094c44da98b954eedeac495271d0f"
  ],
  "network_id": "1",
  "timestamp": "2023-02-10T12:14:05Z",
  "function_selector": "",
  "l1_block_number": 0,
  "l1_timestamp": 0,
  "deposit_tx": false,
  "system_tx": false,
  "mint": null,
  "sig": {
    "v": "0x0",
    "r": "0x0",
    "s": "0x0"
  },
  "transaction_info": {
    "contract_id": "eth:1:0x6b175474e89094c44da98b954eedeac495271d0f",
    "block_number": 16598287,
    "transaction_id": "0x1e44c2d964c9805b235475e55c31c27785aa2fc00129d2a4b21ed5eed6928929",
    "contract_address": "0x6b175474e89094c44da98b954eedeac495271d0f",
    "method": "approve",
    "parameters": null,
    "intrinsic_gas": 21584,
    "refund_gas": 0,
    "call_trace": {
      "hash": "0x1e44c2d964c9805b235475e55c31c27785aa2fc00129d2a4b21ed5eed6928929",
      "contract_name": "Dai",
      "function_name": "approve",
      "function_pc": 2349,
      "function_op": "JUMPDEST",
      "function_file_index": 0,
      "function_code_start": 6228,
      "function_line_number": 149,
      "function_code_length": 179,
      "absolute_position": 84,
      "caller_pc": 0,
      "caller_op": "CALL",
      "call_type": "CALL",
      "from": "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
      "from_balance": "0",
      "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
      "to_balance": "0",
      "value": "0",
      "caller": {
        "address": "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
        "balance": "0"
      },
      "block_timestamp": "0001-01-01T00:00:00Z",
      "gas": 7978416,
      "gas_used": 24514,
      "intrinsic_gas": 21584,
      "input": "0x095ea7b3000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1000000000000000000000000000000000000000000000000000000000000012b",
      "decoded_input": [
        {
          "soltype": {
            "name": "usr",
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
          "value": "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
        },
        {
          "soltype": {
            "name": "wad",
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
          "value": "299"
        }
      ],
      "nonce_diff": [
        {
          "address": "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
          "original": "0",
          "dirty": "1"
        }
      ],
      "state_diff": [
        {
          "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
          "soltype": {
            "name": "allowance",
            "type": "mapping (address => mapping (address => uint256))",
            "storage_location": "storage",
            "components": null,
            "offset": 0,
            "index": "0x0000000000000000000000000000000000000000000000000000000000000003",
            "indexed": false
          },
          "original": {
            "0xdc6bdc37b2714ee601734cf55a05625c9e512461": {
              "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1": "0"
            }
          },
          "dirty": {
            "0xdc6bdc37b2714ee601734cf55a05625c9e512461": {
              "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1": "299"
            }
          },
          "raw": [
            {
              "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
              "key": "0xe11925e259d23a0e30bc90c0742b3349668b7689af7f13b99127b4837cd9c78f",
              "original": "0x0000000000000000000000000000000000000000000000000000000000000000",
              "dirty": "0x000000000000000000000000000000000000000000000000000000000000012b"
            }
          ]
        }
      ],
      "logs": [
        {
          "name": "Approval",
          "anonymous": false,
          "inputs": [
            {
              "soltype": {
                "name": "src",
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
              "value": "0xdc6bdc37b2714ee601734cf55a05625c9e512461"
            },
            {
              "soltype": {
                "name": "guy",
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
              "value": "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
            },
            {
              "soltype": {
                "name": "wad",
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
              "value": "299"
            }
          ],
          "raw": {
            "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "topics": [
              "0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925",
              "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
              "0x000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
            ],
            "data": "0x000000000000000000000000000000000000000000000000000000000000012b"
          }
        }
      ],
      "output": "0x0000000000000000000000000000000000000000000000000000000000000001",
      "decoded_output": [
        {
          "soltype": {
            "name": "",
            "type": "bool",
            "storage_location": "default",
            "components": null,
            "offset": 0,
            "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "indexed": false,
            "simple_type": {
              "type": "bool"
            }
          },
          "value": true
        }
      ],
      "network_id": "1",
      "calls": null
    },
    "stack_trace": null,
    "logs": [
      {
        "name": "Approval",
        "anonymous": false,
        "inputs": [
          {
            "soltype": {
              "name": "src",
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
            "value": "0xdc6bdc37b2714ee601734cf55a05625c9e512461"
          },
          {
            "soltype": {
              "name": "guy",
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
            "value": "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
          },
          {
            "soltype": {
              "name": "wad",
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
            "value": "299"
          }
        ],
        "raw": {
          "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
          "topics": [
            "0x8c5be1e5ebec7d5bd14f71427d1e84f3dd0314c0f7b2291e5b200ac8c7c3b925",
            "0x000000000000000000000000dc6bdc37b2714ee601734cf55a05625c9e512461",
            "0x000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
          ],
          "data": "0x000000000000000000000000000000000000000000000000000000000000012b"
        }
      }
    ],
    "balance_diff": null,
    "nonce_diff": [
      {
        "address": "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
        "original": "0",
        "dirty": "1"
      }
    ],
    "state_diff": [
      {
        "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "soltype": {
          "name": "allowance",
          "type": "mapping (address => mapping (address => uint256))",
          "storage_location": "storage",
          "components": null,
          "offset": 0,
          "index": "0x0000000000000000000000000000000000000000000000000000000000000003",
          "indexed": false
        },
        "original": {
          "0xdc6bdc37b2714ee601734cf55a05625c9e512461": {
            "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1": "0"
          }
        },
        "dirty": {
          "0xdc6bdc37b2714ee601734cf55a05625c9e512461": {
            "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1": "299"
          }
        },
        "raw": [
          {
            "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "key": "0xe11925e259d23a0e30bc90c0742b3349668b7689af7f13b99127b4837cd9c78f",
            "original": "0x0000000000000000000000000000000000000000000000000000000000000000",
            "dirty": "0x000000000000000000000000000000000000000000000000000000000000012b"
          }
        ]
      }
    ],
    "raw_state_diff": null,
    "console_logs": null,
    "created_at": "2023-02-10T12:14:05Z"
  },
  "method": "",
  "decoded_input": null,
  "call_trace": [
    {
      "call_type": "CALL",
      "from": "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
      "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
      "gas": 7978416,
      "gas_used": 24514,
      "type": "CALL",
      "input": "0x095ea7b3000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1000000000000000000000000000000000000000000000000000000000000012b",
      "output": "0x0000000000000000000000000000000000000000000000000000000000000001"
    }
  ]
}

```
{% endtab %}
{% endtabs %}

### Where to go next

For additional information, explore:&#x20;

* [Simulation bundles](bundled-simulations.md) that allow you to simulate several transactions in a bundle such as a sequence of one `approve` and one `transferFrom` transactions.
* [Overriding contract state variables](simulation-api-with-state-overrides.md) showing how to run simulations while overriding contracts' storage slots.
* Advanced usage of Simulation API showing how to simulate on a historical block and extract various portions of simulation results.
* [Using Simulation RPC in dapp UI](../integration-guides/using-simulation-rpc-in-dapp-ui.md) to learn how to display a transaction preview in dapp UI before the user signs it.
