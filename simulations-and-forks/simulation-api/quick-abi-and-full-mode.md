---
description: >-
  Use Simulation API in full mode for complete decoding of transaction outputs,
  abi for partial decoding of transaction info, or go with quick mode for faster
  response times and raw transaction outputs.
---

# Quick, Abi and Full Mode

Use the `simulation_type` parameter to opt for quick, abi, or full simulation API mode.&#x20;

* **Select quick simulations** when you need minimal, raw values.
* **Use abi simulations** when you need minimal information with decoded inputs, outputs, and logs.
* **Go with full simulations** when you need raw and decoded information. Full simulations attach Solidity types to the raw simulation response so you don't have to decode the information on your own. For example, raw call data (transaction's data field) is decoded to the argument names defined in the contract's smart code.



Abi simulations response will contain the following information:

* The **call trace** containing the function name decoded input, and output variables
* Decoded **logs (events)** consisting of the Solidity **event** that produced them and the event arguments' **value**, enriched with **type** description for each.



Full simulations decode the following information:&#x20;

* The **call trace** containing the function name, position in the source file, caller's address, and  balance
* Decoded **function inputs and outputs**, with **soltype** for all arguments. This applies to all function calls, including the direct call to the smart contract from EOA, internal calls between smart contracts, and function calls within each smart contract.
* Decoded **state diff** (changes to the state) enriched with **soltype** for the modified fields
* Decoded **logs (events)** consisting of the Solidity **event** that produced them and the event arguments' **value**, enriched with **type** for each.

{% hint style="info" %}
* Full simulations take more time, depending on the depth of the call trace.
* When decoded information isn't necessary, the best performance is achieved with quick simulations.
{% endhint %}

{% tabs %}
{% tab title="Quick Request" %}
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
      simulation_type: 'quick', // full or quick (full is default)

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

{% tab title="Quick Result" %}
```
Simulation: 179.03ms
{
  "hash": "0x1e44c2d964c9805b235475e55c31c27785aa2fc00129d2a4b21ed5eed6928929",
  "block_hash": "",
  "block_number": 16598226,
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
  "addresses": null,
  "contract_ids": null,
  "network_id": "1",
  "timestamp": "2023-02-10T12:01:58Z",
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
    "block_number": 16598226,
    "transaction_id": "0x1e44c2d964c9805b235475e55c31c27785aa2fc00129d2a4b21ed5eed6928929",
    "contract_address": "0x6b175474e89094c44da98b954eedeac495271d0f",
    "method": null,
    "parameters": null,
    "intrinsic_gas": 21584,
    "refund_gas": 0,
    "call_trace": {
      "hash": "0x1e44c2d964c9805b235475e55c31c27785aa2fc00129d2a4b21ed5eed6928929",
      "contract_name": "",
      "function_pc": 0,
      "function_op": "CALL",
      "absolute_position": 0,
      "caller_pc": 0,
      "caller_op": "CALL",
      "call_type": "CALL",
      "from": "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
      "from_balance": "0",
      "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
      "to_balance": "0",
      "value": "0",
      "block_timestamp": "0001-01-01T00:00:00Z",
      "gas": 7978416,
      "gas_used": 24514,
      "intrinsic_gas": 21584,
      "input": "0x095ea7b3000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1000000000000000000000000000000000000000000000000000000000000012b",
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
          "soltype": null,
          "original": null,
          "dirty": null,
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
          "name": "",
          "anonymous": false,
          "inputs": null,
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
      "decoded_output": null,
      "network_id": "1",
      "calls": null
    },
    "stack_trace": null,
    "logs": [
      {
        "name": "",
        "anonymous": false,
        "inputs": null,
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
        "soltype": null,
        "original": null,
        "dirty": null,
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
    "created_at": "2023-02-10T12:01:58Z"
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

{% tab title="Full Request" %}
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

{% tab title="Full result" %}
```
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

{% tab title="Diff" %}
```diff
diff --git a/testing-tenderly-hardhat-ts/samples/approve-dai-quick-api.txt b/testing-tenderly-hardhat-ts/samples/approve-dai-full-api.txt
index f247b98..064bd97 100644
--- QUICK
+++ FULL
@@ -1,8 +1,8 @@
-Simulation: 226.380ms
+Simulation: 206.636ms
 {
   "hash": "0x1e44c2d964c9805b235475e55c31c27785aa2fc00129d2a4b21ed5eed6928929",
   "block_hash": "",
-  "block_number": 16569006,
+  "block_number": 16569009,
   "from": "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
   "gas": 8000000,
   "gas_price": 0,
@@ -18,10 +18,16 @@ Simulation: 226.380ms
   "value": "0x",
   "access_list": null,
   "status": true,
-  "addresses": null,
-  "contract_ids": null,
+  "addresses": [
+    "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
+    "0x6b175474e89094c44da98b954eedeac495271d0f"
+  ],
+  "contract_ids": [
+    "eth:1:0xdc6bdc37b2714ee601734cf55a05625c9e512461",
+    "eth:1:0x6b175474e89094c44da98b954eedeac495271d0f"
+  ],
   "network_id": "1",
-  "timestamp": "2023-02-06T09:59:49Z",
+  "timestamp": "2023-02-06T10:00:35Z",
   "function_selector": "",
   "l1_block_number": 0,
   "l1_timestamp": 0,
@@ -35,19 +41,24 @@ Simulation: 226.380ms
   },
   "transaction_info": {
     "contract_id": "eth:1:0x6b175474e89094c44da98b954eedeac495271d0f",
-    "block_number": 16569007,
+    "block_number": 16569010,
     "transaction_id": "0x1e44c2d964c9805b235475e55c31c27785aa2fc00129d2a4b21ed5eed6928929",
     "contract_address": "0x6b175474e89094c44da98b954eedeac495271d0f",
-    "method": null,
+    "method": "approve",
     "parameters": null,
     "intrinsic_gas": 21584,
     "refund_gas": 0,
     "call_trace": {
       "hash": "0x1e44c2d964c9805b235475e55c31c27785aa2fc00129d2a4b21ed5eed6928929",
-      "contract_name": "",
-      "function_pc": 0,
-      "function_op": "CALL",
-      "absolute_position": 0,
+      "contract_name": "Dai",
+      "function_name": "approve",
+      "function_pc": 2349,
+      "function_op": "JUMPDEST",
+      "function_file_index": 0,
+      "function_code_start": 6228,
+      "function_line_number": 149,
+      "function_code_length": 179,
+      "absolute_position": 84,
       "caller_pc": 0,
       "caller_op": "CALL",
       "call_type": "CALL",
@@ -56,11 +67,47 @@ Simulation: 226.380ms
       "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
       "to_balance": "0",
       "value": "0",
+      "caller": {
+        "address": "0xdc6bdc37b2714ee601734cf55a05625c9e512461",
+        "balance": "0"
+      },
       "block_timestamp": "0001-01-01T00:00:00Z",
       "gas": 7978416,
       "gas_used": 24514,
       "intrinsic_gas": 21584,
       "input": "0x095ea7b3000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1000000000000000000000000000000000000000000000000000000000000012b",
+      "decoded_input": [
+        {
+          "soltype": {
+            "name": "usr",
+            "type": "address",
+            "storage_location": "default",
+            "components": null,
+            "offset": 0,
+            "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
+            "indexed": false,
+            "simple_type": {
+              "type": "address"
+            }
+          },
+          "value": "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
+        },
+        {
+          "soltype": {
+            "name": "wad",
+            "type": "uint256",
+            "storage_location": "default",
+            "components": null,
+            "offset": 0,
+            "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
+            "indexed": false,
+            "simple_type": {
+              "type": "uint"
+            }
+          },
+          "value": "299"
+        }
+      ],
       "nonce_diff": [
         {
           "address": "0xDC6bDc37B2714eE601734cf55A05625C9e512461",
@@ -71,9 +118,25 @@ Simulation: 226.380ms
       "state_diff": [
         {
           "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
-          "soltype": null,
-          "original": null,
-          "dirty": null,
+          "soltype": {
+            "name": "allowance",
+            "type": "mapping (address => mapping (address => uint256))",
+            "storage_location": "storage",
+            "components": null,
+            "offset": 0,
+            "index": "0x0000000000000000000000000000000000000000000000000000000000000003",
+            "indexed": false
+          },
+          "original": {
+            "0xdc6bdc37b2714ee601734cf55a05625c9e512461": {
+              "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1": "0"
+            }
+          },
+          "dirty": {
+            "0xdc6bdc37b2714ee601734cf55a05625c9e512461": {
+              "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1": "299"
+            }
+          },
           "raw": [
             {
               "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
@@ -86,9 +149,55 @@ Simulation: 226.380ms
       ],
       "logs": [
         {
-          "name": "",
+          "name": "Approval",
           "anonymous": false,
-          "inputs": null,
+          "inputs": [
+            {
+              "soltype": {
+                "name": "src",
+                "type": "address",
+                "storage_location": "default",
+                "components": null,
+                "offset": 0,
+                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
+                "indexed": true,
+                "simple_type": {
+                  "type": "address"
+                }
+              },
+              "value": "0xdc6bdc37b2714ee601734cf55a05625c9e512461"
+            },
+            {
+              "soltype": {
+                "name": "guy",
+                "type": "address",
+                "storage_location": "default",
+                "components": null,
+                "offset": 0,
+                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
+                "indexed": true,
+                "simple_type": {
+                  "type": "address"
+                }
+              },
+              "value": "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
+            },
+            {
+              "soltype": {
+                "name": "wad",
+                "type": "uint256",
+                "storage_location": "default",
+                "components": null,
+                "offset": 0,
+                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
+                "indexed": false,
+                "simple_type": {
+                  "type": "uint"
+                }
+              },
+              "value": "299"
+            }
+          ],
           "raw": {
             "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
             "topics": [
@@ -101,16 +210,78 @@ Simulation: 226.380ms
         }
       ],
       "output": "0x0000000000000000000000000000000000000000000000000000000000000001",
-      "decoded_output": null,
+      "decoded_output": [
+        {
+          "soltype": {
+            "name": "",
+            "type": "bool",
+            "storage_location": "default",
+            "components": null,
+            "offset": 0,
+            "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
+            "indexed": false,
+            "simple_type": {
+              "type": "bool"
+            }
+          },
+          "value": true
+        }
+      ],
       "network_id": "1",
       "calls": null
     },
     "stack_trace": null,
     "logs": [
       {
-        "name": "",
+        "name": "Approval",
         "anonymous": false,
-        "inputs": null,
+        "inputs": [
+          {
+            "soltype": {
+              "name": "src",
+              "type": "address",
+              "storage_location": "default",
+              "components": null,
+              "offset": 0,
+              "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
+              "indexed": true,
+              "simple_type": {
+                "type": "address"
+              }
+            },
+            "value": "0xdc6bdc37b2714ee601734cf55a05625c9e512461"
+          },
+          {
+            "soltype": {
+              "name": "guy",
+              "type": "address",
+              "storage_location": "default",
+              "components": null,
+              "offset": 0,
+              "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
+              "indexed": true,
+              "simple_type": {
+                "type": "address"
+              }
+            },
+            "value": "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1"
+          },
+          {
+            "soltype": {
+              "name": "wad",
+              "type": "uint256",
+              "storage_location": "default",
+              "components": null,
+              "offset": 0,
+              "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
+              "indexed": false,
+              "simple_type": {
+                "type": "uint"
+              }
+            },
+            "value": "299"
+          }
+        ],
         "raw": {
           "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
           "topics": [
@@ -133,9 +304,25 @@ Simulation: 226.380ms
     "state_diff": [
       {
         "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
-        "soltype": null,
-        "original": null,
-        "dirty": null,
+        "soltype": {
+          "name": "allowance",
+          "type": "mapping (address => mapping (address => uint256))",
+          "storage_location": "storage",
+          "components": null,
+          "offset": 0,
+          "index": "0x0000000000000000000000000000000000000000000000000000000000000003",
+          "indexed": false
+        },
+        "original": {
+          "0xdc6bdc37b2714ee601734cf55a05625c9e512461": {
+            "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1": "0"
+          }
+        },
+        "dirty": {
+          "0xdc6bdc37b2714ee601734cf55a05625c9e512461": {
+            "0xf1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1": "299"
+          }
+        },
         "raw": [
           {
             "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
@@ -148,7 +335,7 @@ Simulation: 226.380ms
     ],
     "raw_state_diff": null,
     "console_logs": null,
-    "created_at": "2023-02-06T09:59:49Z"
+    "created_at": "2023-02-06T10:00:35Z"
   },
   "method": "",
   "decoded_input": null,

```
{% endtab %}
{% endtabs %}
