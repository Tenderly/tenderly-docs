---
description: Learn how to use state overrides to modify smart contract states.
---

# Simulation API With State Overrides

State overrides allow you to modify smart contracts' states for the duration of a simulation. This allows you to specify a particular state for the contracts included in the transaction you're simulating. This way, you can execute a highly specific simulation scenario.

To specify the override, assign `SimulationRequest.state_objects` to the map of overrides. The `SimulationRequest.state_objects.["0x6b17...1d0f"].storage` is the mapping from a [smart contract's storage locations](https://docs.soliditylang.org/en/latest/internals/layout\_in\_storage.html#mappings-and-dynamic-arrays) to a value override that will be applied to the blockchain history, prior to running the simulation.

The following example shows how an arbitrary sender `0xe2e2...e2` calls the `mint` function of the [DAI Mainnet contract (`0x6b17...71d0f`)](https://dashboard.tenderly.co/contract/mainnet/0x6b175474e89094c44da98b954eedeac495271d0f). In order to mint, the sender of the transaction must be a ward. In other words, the following condition must hold:

```
wards['0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2'] == 1
```

You can simulate the call to the mint function while instructing Tenderly to override that particular `wards[$sender]` entry to the value of 1 (at the length of 32 bytes) so the condition holds.

The override has to be supplied to the storage location of `$sender` relative to the storage slot of `wards` – the 0th slot in the DAI smart contract. This is the way to obtain it:

$$
{keccak_{256} \lparen \underbrace{\tt{0xf2...f2}}_\text{\tt{sender}, 20B}\ .\ \underbrace{\tt{0x00..00}}_\text{\tt{wards} slot, 32B}\rparen}
$$

In our case, this evaluates to `0xedd7d04419e9c48ceb6055956cbb4e2091ae310313a4d1fa7cbcfe7561616e03`. The override map `state_object` looks like this for the DAI contract:

```json
"state_objects": {
  "0x6b175474e89094c44da98b954eedeac495271d0f": {
    // DAI contract storage overrides
    "storage": {
      // wards['0xdc6b...2461'] gets assigned 1
      "0xedd7d04419e9c48ceb6055956cbb4e2091ae310313a4d1fa7cbcfe7561616e03":
        "0x0000000000000000000000000000000000000000000000000000000000000001",
    },
  },
},
```

{% tabs %}
{% tab title="API Request" %}
```typescript
import axios from 'axios';
import * as dotenv from 'dotenv';
import { ethers } from 'ethers';
dotenv.config();

// assuming environment variables TENDERLY_USER, TENDERLY_PROJECT and TENDERLY_ACCESS_KEY are set
// https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name
// https://docs.tenderly.co/other/platform-access/how-to-generate-api-access-tokens
const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;

const mintDai = async () => {
  console.time('Simulation');
  const wardAddress = '0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2';
  // calculte the storage location of `wards[wardAddress]`
  // yields 0xedd7d04419e9c48ceb6055956cbb4e2091ae310313a4d1fa7cbcfe7561616e03
  const overrideStorageLocation = ethers.utils.keccak256(
    ethers.utils.concat([
      ethers.utils.hexZeroPad(wardAddress, 32), // the ward address (address 0x000..0) - mapping key
      ethers.utils.hexZeroPad('0x0', 32), // the wards slot is 0th  in the DAI contract - the mapping variable
    ])
  );
  console.log('Storage Override Location', overrideStorageLocation);
  const mint = (
    await axios.post(
      `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/simulate`,
      // the transaction
      {
        save: true,
        save_if_fails: true,
        simulation_type: 'full',
        network_id: '1',
        from: '0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2',
        to: '0x6b175474e89094c44da98b954eedeac495271d0f',
        input:
          '0x40c10f19000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce10000000000000000000000000000000000000000000000001bc16d674ec80000',
        gas: 8000000,
        state_objects: {
          '0x6b175474e89094c44da98b954eedeac495271d0f': {
            storage: {
              '0xedd7d04419e9c48ceb6055956cbb4e2091ae310313a4d1fa7cbcfe7561616e03':
                '0x0000000000000000000000000000000000000000000000000000000000000001',
            },
          },
        },
      },
      {
        headers: {
          'X-Access-Key': TENDERLY_ACCESS_KEY as string,
        },
      }
    )
  ).data;

  console.timeEnd('Simulation');
  console.log(JSON.stringify(mint, null, 2));
  // TODO: extract token transferred
};


mintDai();

```
{% endtab %}

{% tab title="API Response" %}
```json
Storage Override Location 0xedd7d04419e9c48ceb6055956cbb4e2091ae310313a4d1fa7cbcfe7561616e03
Simulation: 185.029ms
{
  "transaction": {
    "hash": "0xd9d52b2cb6b6d8d8640bc2dee86050a623401fe39d7fbc4ab46ffd7ff3ea6ab6",
    "block_hash": "",
    "block_number": 16598541,
    "from": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
    "gas": 8000000,
    "gas_price": 0,
    "gas_fee_cap": 0,
    "gas_tip_cap": 0,
    "cumulative_gas_used": 0,
    "gas_used": 53465,
    "effective_gas_price": 0,
    "input": "0x40c10f19000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce10000000000000000000000000000000000000000000000001bc16d674ec80000",
    "nonce": 0,
    "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
    "index": 0,
    "value": "0x",
    "access_list": null,
    "status": true,
    "addresses": [
      "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
      "0x6b175474e89094c44da98b954eedeac495271d0f"
    ],
    "contract_ids": [
      "eth:1:0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
      "eth:1:0x6b175474e89094c44da98b954eedeac495271d0f"
    ],
    "network_id": "1",
    "timestamp": "2023-02-10T13:04:56Z",
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
      "block_number": 16598541,
      "transaction_id": "0xd9d52b2cb6b6d8d8640bc2dee86050a623401fe39d7fbc4ab46ffd7ff3ea6ab6",
      "contract_address": "0x6b175474e89094c44da98b954eedeac495271d0f",
      "method": "mint",
      "parameters": null,
      "intrinsic_gas": 21620,
      "refund_gas": 0,
      "call_trace": {
        "hash": "0xd9d52b2cb6b6d8d8640bc2dee86050a623401fe39d7fbc4ab46ffd7ff3ea6ab6",
        "contract_name": "Dai",
        "function_name": "mint",
        "function_pc": 3948,
        "function_op": "JUMPDEST",
        "function_file_index": 0,
        "function_code_start": 5501,
        "function_line_number": 134,
        "function_code_length": 202,
        "absolute_position": 88,
        "caller_pc": 0,
        "caller_op": "CALL",
        "call_type": "CALL",
        "from": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
        "from_balance": "0",
        "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "to_balance": "0",
        "value": "0",
        "caller": {
          "address": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
          "balance": "0"
        },
        "block_timestamp": "0001-01-01T00:00:00Z",
        "gas": 7978380,
        "gas_used": 31845,
        "intrinsic_gas": 21620,
        "input": "0x40c10f19000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce10000000000000000000000000000000000000000000000001bc16d674ec80000",
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
            "value": "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1"
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
            "value": "2000000000000000000"
          }
        ],
        "nonce_diff": [
          {
            "address": "0xe2E2E2e2e2e2E2E2E2E2e2E2e2E2E2e2e2e2E2e2",
            "original": "0",
            "dirty": "1"
          }
        ],
        "state_diff": [
          {
            "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "soltype": {
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
            "original": "5090814826520179690761462859",
            "dirty": "5090814828520179690761462859",
            "raw": [
              {
                "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
                "key": "0x0000000000000000000000000000000000000000000000000000000000000001",
                "original": "0x0000000000000000000000000000000000000000107305f8bb52a43b529da44b",
                "dirty": "0x0000000000000000000000000000000000000000107305f8d71411a2a165a44b"
              }
            ]
          },
          {
            "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "soltype": {
              "name": "balanceOf",
              "type": "mapping (address => uint256)",
              "storage_location": "storage",
              "components": null,
              "offset": 0,
              "index": "0x0000000000000000000000000000000000000000000000000000000000000002",
              "indexed": false
            },
            "original": {
              "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1": "0"
            },
            "dirty": {
              "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1": "2000000000000000000"
            },
            "raw": [
              {
                "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
                "key": "0x9b5472766fd311751f6a33c8e30061e20a26259ca626cf5a2feaadf96903cd9e",
                "original": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "dirty": "0x0000000000000000000000000000000000000000000000001bc16d674ec80000"
              }
            ]
          }
        ],
        "logs": [
          {
            "name": "Transfer",
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
                "value": "0x0000000000000000000000000000000000000000"
              },
              {
                "soltype": {
                  "name": "dst",
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
                "value": "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1"
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
                "value": "2000000000000000000"
              }
            ],
            "raw": {
              "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
              "topics": [
                "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                "0x0000000000000000000000000000000000000000000000000000000000000000",
                "0x000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce1"
              ],
              "data": "0x0000000000000000000000000000000000000000000000001bc16d674ec80000"
            }
          }
        ],
        "output": "0x",
        "decoded_output": null,
        "network_id": "1",
        "calls": [
          {
            "hash": "",
            "contract_name": "Dai",
            "function_name": "add",
            "function_pc": 7825,
            "function_op": "JUMPDEST",
            "function_file_index": 0,
            "function_code_start": 3853,
            "function_line_number": 94,
            "function_code_length": 102,
            "absolute_position": 136,
            "caller_pc": 4200,
            "caller_op": "JUMP",
            "caller_file_index": 0,
            "caller_line_number": 135,
            "caller_code_start": 5579,
            "caller_code_length": 24,
            "call_type": "JUMPDEST",
            "from": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "from_balance": null,
            "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "to_balance": null,
            "value": null,
            "caller": {
              "address": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
              "balance": "0"
            },
            "block_timestamp": "0001-01-01T00:00:00Z",
            "gas": 7973640,
            "gas_used": 62,
            "input": "0x",
            "decoded_input": [
              {
                "soltype": {
                  "name": "x",
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
                "value": "0"
              },
              {
                "soltype": {
                  "name": "y",
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
                "value": "2000000000000000000"
              }
            ],
            "output": "0x",
            "decoded_output": [
              {
                "soltype": {
                  "name": "z",
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
                "value": "2000000000000000000"
              }
            ],
            "network_id": "",
            "calls": null
          },
          {
            "hash": "",
            "contract_name": "Dai",
            "function_name": "add",
            "function_pc": 7825,
            "function_op": "JUMPDEST",
            "function_file_index": 0,
            "function_code_start": 3853,
            "function_line_number": 94,
            "function_code_length": 102,
            "absolute_position": 184,
            "caller_pc": 4279,
            "caller_op": "JUMP",
            "caller_file_index": 0,
            "caller_line_number": 136,
            "caller_code_start": 5630,
            "caller_code_length": 21,
            "call_type": "JUMPDEST",
            "from": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "from_balance": null,
            "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "to_balance": null,
            "value": null,
            "caller": {
              "address": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
              "balance": "0"
            },
            "block_timestamp": "0001-01-01T00:00:00Z",
            "gas": 7951356,
            "gas_used": 62,
            "input": "0x",
            "decoded_input": [
              {
                "soltype": {
                  "name": "x",
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
                "value": "5090814826520179690761462859"
              },
              {
                "soltype": {
                  "name": "y",
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
                "value": "2000000000000000000"
              }
            ],
            "output": "0x",
            "decoded_output": [
              {
                "soltype": {
                  "name": "z",
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
                "value": "5090814828520179690761462859"
              }
            ],
            "network_id": "",
            "calls": null
          }
        ]
      },
      "stack_trace": null,
      "logs": [
        {
          "name": "Transfer",
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
              "value": "0x0000000000000000000000000000000000000000"
            },
            {
              "soltype": {
                "name": "dst",
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
              "value": "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1"
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
              "value": "2000000000000000000"
            }
          ],
          "raw": {
            "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
            "topics": [
              "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
              "0x0000000000000000000000000000000000000000000000000000000000000000",
              "0x000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce1"
            ],
            "data": "0x0000000000000000000000000000000000000000000000001bc16d674ec80000"
          }
        }
      ],
      "balance_diff": null,
      "nonce_diff": [
        {
          "address": "0xe2E2E2e2e2e2E2E2E2E2e2E2e2E2E2e2e2e2E2e2",
          "original": "0",
          "dirty": "1"
        }
      ],
      "state_diff": [
        {
          "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
          "soltype": {
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
          "original": "5090814826520179690761462859",
          "dirty": "5090814828520179690761462859",
          "raw": [
            {
              "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
              "key": "0x0000000000000000000000000000000000000000000000000000000000000001",
              "original": "0x0000000000000000000000000000000000000000107305f8bb52a43b529da44b",
              "dirty": "0x0000000000000000000000000000000000000000107305f8d71411a2a165a44b"
            }
          ]
        },
        {
          "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
          "soltype": {
            "name": "balanceOf",
            "type": "mapping (address => uint256)",
            "storage_location": "storage",
            "components": null,
            "offset": 0,
            "index": "0x0000000000000000000000000000000000000000000000000000000000000002",
            "indexed": false
          },
          "original": {
            "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1": "0"
          },
          "dirty": {
            "0xe58b9ee93700a616b50509c8292977fa7a0f8ce1": "2000000000000000000"
          },
          "raw": [
            {
              "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
              "key": "0x9b5472766fd311751f6a33c8e30061e20a26259ca626cf5a2feaadf96903cd9e",
              "original": "0x0000000000000000000000000000000000000000000000000000000000000000",
              "dirty": "0x0000000000000000000000000000000000000000000000001bc16d674ec80000"
            }
          ]
        }
      ],
      "raw_state_diff": null,
      "console_logs": null,
      "created_at": "2023-02-10T13:04:56Z"
    },
    "method": "",
    "decoded_input": null,
    "call_trace": [
      {
        "call_type": "CALL",
        "from": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
        "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
        "gas": 7978380,
        "gas_used": 31845,
        "type": "CALL",
        "input": "0x40c10f19000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce10000000000000000000000000000000000000000000000001bc16d674ec80000"
      }
    ]
  },
  "simulation": {
    "id": "46cb1f92-c9ee-4ef2-8736-6dc6ae84f8d8",
    "project_id": "11686306-12f4-4c48-9396-c07dbe6b3c51",
    "owner_id": "796e7d91-d8a2-4137-af6c-361f34e79557",
    "network_id": "1",
    "block_number": 16598541,
    "transaction_index": 0,
    "from": "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
    "to": "0x6b175474e89094c44da98b954eedeac495271d0f",
    "input": "0x40c10f19000000000000000000000000e58b9ee93700a616b50509c8292977fa7a0f8ce10000000000000000000000000000000000000000000000001bc16d674ec80000",
    "gas": 8000000,
    "gas_price": "0",
    "gas_used": 53465,
    "value": "0",
    "method": "mint",
    "status": true,
    "access_list": null,
    "queue_origin": "",
    "block_header": {
      "number": "0xfd460d",
      "hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "stateRoot": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "parentHash": "0x033362dcc958b7c9628256b1a59d7a82c2a7205fc7cb7c3270d08aef8e760e52",
      "sha3Uncles": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "transactionsRoot": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "receiptsRoot": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
      "timestamp": "0x63e640f8",
      "difficulty": "0x0",
      "gasLimit": "0x1c9c380",
      "gasUsed": "0xed3d6a",
      "miner": "0x0000000000000000000000000000000000000000",
      "extraData": "0x",
      "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
      "nonce": "0x0000000000000000",
      "baseFeePerGas": "0x1",
      "size": "0x0",
      "totalDifficulty": "0x0",
      "uncles": null,
      "transactions": null
    },
    "state_overrides": {
      "0x6b175474e89094c44da98b954eedeac495271d0f": {
        "storage": {
          "0xedd7d04419e9c48ceb6055956cbb4e2091ae310313a4d1fa7cbcfe7561616e03": "0x0000000000000000000000000000000000000000000000000000000000000001"
        }
      }
    },
    "mint": null,
    "deposit_tx": false,
    "system_tx": false,
    "nonce": 0,
    "addresses": [
      "0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
      "0x6b175474e89094c44da98b954eedeac495271d0f"
    ],
    "contract_ids": [
      "eth:1:0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2",
      "eth:1:0x6b175474e89094c44da98b954eedeac495271d0f"
    ],
    "created_at": "2023-02-10T13:04:57.004109816Z"
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
        "symbol": "DAI",
        "name": "Dai Stablecoin",
        "decimals": 18,
        "main": true
      },
      "evm_version": "default",
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
            "name": "totalSupply",
            "constant": true,
            "anonymous": false,
            "stateMutability": "view",
            "inputs": [],
            "outputs": [
              {
                "name": "",
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
            "name": "move",
            "constant": false,
            "anonymous": false,
            "stateMutability": "nonpayable",
            "inputs": [
              {
                "name": "src",
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
                "name": "dst",
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
              }
            ],
            "outputs": []
          },
          {
            "type": "function",
            "name": "name",
            "constant": true,
            "anonymous": false,
            "stateMutability": "view",
            "inputs": [],
            "outputs": [
              {
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
              }
            ]
          },
          {
            "type": "function",
            "name": "wards",
            "constant": true,
            "anonymous": false,
            "stateMutability": "view",
            "inputs": [
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
            ],
            "outputs": [
              {
                "name": "",
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
            "name": "approve",
            "constant": false,
            "anonymous": false,
            "stateMutability": "nonpayable",
            "inputs": [
              {
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
              {
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
              }
            ],
            "outputs": [
              {
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
              }
            ]
          },
          {
            "type": "function",
            "name": "mint",
            "constant": false,
            "anonymous": false,
            "stateMutability": "nonpayable",
            "inputs": [
              {
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
              {
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
              }
            ],
            "outputs": []
          },
          {
            "type": "function",
            "name": "transferFrom",
            "constant": false,
            "anonymous": false,
            "stateMutability": "nonpayable",
            "inputs": [
              {
                "name": "src",
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
                "name": "dst",
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
              }
            ],
            "outputs": [
              {
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
              }
            ]
          },
          {
            "type": "function",
            "name": "burn",
            "constant": false,
            "anonymous": false,
            "stateMutability": "nonpayable",
            "inputs": [
              {
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
              {
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
              }
            ],
            "outputs": []
          },
          {
            "type": "function",
            "name": "deny",
            "constant": false,
            "anonymous": false,
            "stateMutability": "nonpayable",
            "inputs": [
              {
                "name": "guy",
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
            "name": "push",
            "constant": false,
            "anonymous": false,
            "stateMutability": "nonpayable",
            "inputs": [
              {
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
              {
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
              }
            ],
            "outputs": []
          },
          {
            "type": "function",
            "name": "nonces",
            "constant": true,
            "anonymous": false,
            "stateMutability": "view",
            "inputs": [
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
            ],
            "outputs": [
              {
                "name": "",
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
            "name": "symbol",
            "constant": true,
            "anonymous": false,
            "stateMutability": "view",
            "inputs": [],
            "outputs": [
              {
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
              }
            ]
          },
          {
            "type": "function",
            "name": "allowance",
            "constant": true,
            "anonymous": false,
            "stateMutability": "view",
            "inputs": [
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
              },
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
            ],
            "outputs": [
              {
                "name": "",
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
            "name": "balanceOf",
            "constant": true,
            "anonymous": false,
            "stateMutability": "view",
            "inputs": [
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
            ],
            "outputs": [
              {
                "name": "",
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
            "name": "version",
            "constant": true,
            "anonymous": false,
            "stateMutability": "view",
            "inputs": [],
            "outputs": [
              {
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
              }
            ]
          },
          {
            "type": "function",
            "name": "PERMIT_TYPEHASH",
            "constant": true,
            "anonymous": false,
            "stateMutability": "view",
            "inputs": [],
            "outputs": [
              {
                "name": "",
                "type": "bytes32",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "bytes"
                }
              }
            ]
          },
          {
            "type": "function",
            "name": "transfer",
            "constant": false,
            "anonymous": false,
            "stateMutability": "nonpayable",
            "inputs": [
              {
                "name": "dst",
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
              }
            ],
            "outputs": [
              {
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
              }
            ]
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
          },
          {
            "type": "function",
            "name": "DOMAIN_SEPARATOR",
            "constant": true,
            "anonymous": false,
            "stateMutability": "view",
            "inputs": [],
            "outputs": [
              {
                "name": "",
                "type": "bytes32",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "bytes"
                }
              }
            ]
          },
          {
            "type": "function",
            "name": "permit",
            "constant": false,
            "anonymous": false,
            "stateMutability": "nonpayable",
            "inputs": [
              {
                "name": "holder",
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
                "name": "spender",
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
                "name": "nonce",
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
                "name": "expiry",
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
                "name": "allowed",
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
              {
                "name": "v",
                "type": "uint8",
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
                "name": "r",
                "type": "bytes32",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": false,
                "simple_type": {
                  "type": "bytes"
                }
              },
              {
                "name": "s",
                "type": "bytes32",
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
            "outputs": []
          },
          {
            "type": "function",
            "name": "pull",
            "constant": false,
            "anonymous": false,
            "stateMutability": "nonpayable",
            "inputs": [
              {
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
              {
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
              }
            ],
            "outputs": []
          },
          {
            "type": "function",
            "name": "rely",
            "constant": false,
            "anonymous": false,
            "stateMutability": "nonpayable",
            "inputs": [
              {
                "name": "guy",
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
            "type": "event",
            "name": "Approval",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": [
              {
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
              {
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
              {
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
              }
            ],
            "outputs": null
          },
          {
            "type": "event",
            "name": "LogNote",
            "constant": false,
            "anonymous": true,
            "stateMutability": "",
            "inputs": [
              {
                "name": "sig",
                "type": "bytes4",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": true,
                "simple_type": {
                  "type": "bytes"
                }
              },
              {
                "name": "usr",
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
                "name": "arg1",
                "type": "bytes32",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": true,
                "simple_type": {
                  "type": "bytes"
                }
              },
              {
                "name": "arg2",
                "type": "bytes32",
                "storage_location": "default",
                "components": null,
                "offset": 0,
                "index": "0x0000000000000000000000000000000000000000000000000000000000000000",
                "indexed": true,
                "simple_type": {
                  "type": "bytes"
                }
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
            "outputs": null
          },
          {
            "type": "event",
            "name": "Transfer",
            "constant": false,
            "anonymous": false,
            "stateMutability": "",
            "inputs": [
              {
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
              {
                "name": "dst",
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
              }
            ],
            "outputs": null
          }
        ],
        "raw_abi": null,
        "states": [
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
          },
          {
            "name": "nonces",
            "type": "mapping (address => uint256)",
            "storage_location": "storage",
            "components": null,
            "offset": 0,
            "index": "0x0000000000000000000000000000000000000000000000000000000000000004",
            "indexed": false
          }
        ]
      },
      "creation_block": 0,
      "creation_tx": "",
      "creator_address": "",
      "created_at": "2022-12-16T09:10:37Z",
      "number_of_watches": null,
      "language": "solidity",
      "in_project": false,
      "number_of_files": 1
    }
  ],
  "generated_access_list": []
}

```
{% endtab %}
{% endtabs %}
