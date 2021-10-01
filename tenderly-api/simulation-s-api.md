# Simulation\(s\) API

## API Authentication

You can read more about API authentication here: [Authenticating with the Tenderly API](authenticating-with-the-tenderly-api.md).

## Simulate API

The rest of this document assumes you have authenticated with one of the two previously mentioned methods.

Because the Simulate API supports saving simulations, you will need to specify a project when calling the API. The project is determined by the `project_slug` path parameter. You can find the slug for you project in the address bar:

![](../.gitbook/assets/image%20%2852%29.png)

**Link**: \*\*\*\*`https://api.tenderly.co/api/v1/account/me/project/{{project_slug}}/simulate`

**Request Type**: `POST`

**Payload**:

{% hint style="info" %}
The simulate payload is similar to the [eth\_call](https://github.com/ethereum/wiki/wiki/json-rpc#eth_call) JSON RPC call.
{% endhint %}

```text
{
    "network_id": "1",
    "block_number": 15107216,
    "transaction_index": 1,
    "from": "0x0000000000000000000000000000000000000012",
    "to": "0x0000000000000000000000000000000000000000",
    "input": "0x",
    "gas": 10000000,
    "gas_price": "0",
    "value": 0,
    "save": true,
		"save_if_fails": false
}
```

**Payload explanation**:

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Mandatory Y/N</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">network_id</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">
        <p>The network on which you want the simulate the transaction. One of:
          <br
          />
        </p>
        <ul>
          <li>Mainnet: 1</li>
          <li>Ropsten: 3</li>
          <li>Rinkeby: 4</li>
          <li>Goerli: 5</li>
          <li>Kovan: 42</li>
        </ul>
      </td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left">block_number</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">Block height. If left out the latest block will be used.</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">transaction_index</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">The index of the transaction inside the block.
        <br />
        <br />Note: This parameter must be omitted or 0 when the block_number property
        is left out.</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">from</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The originating address for the simulated transaction.</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left">to</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The destination address for the simulated transaction.</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left">input</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">ABI encoded input for the transaction.</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left">gas</td>
      <td style="text-align:left">number</td>
      <td style="text-align:left">The gas limit for the transaction.</td>
      <td style="text-align:left">Y</td>
    </tr>
    <tr>
      <td style="text-align:left">gas_price</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The gas price for the transaction.</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">value</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">The ETH value sent in the transaction.</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">simulation_type</td>
      <td style="text-align:left">string</td>
      <td style="text-align:left">Either <em>full</em> or <em>quick</em>. <em>full</em> simulations use the contracts
        source code to generate a full trace, while the <em>quick</em> simulation
        will only use the contracts bytecode. If omitted, the default value is <em>full.</em>
      </td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">save</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">Whether or not to save this simulation for later inspection.</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">save_if_fails</td>
      <td style="text-align:left">boolean</td>
      <td style="text-align:left">Save the simulation if the simulated transaction failed.</td>
      <td style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">state_objects</td>
      <td style="text-align:left">map[address]StateObject</td>
      <td style="text-align:left">Use provided state objects to overwrite current state objects at <b>address</b>.</td>
      <td
      style="text-align:left">N</td>
    </tr>
    <tr>
      <td style="text-align:left">contracts</td>
      <td style="text-align:left">[]Contract</td>
      <td style="text-align:left">Array of contract deployment info (exactly like contract upload requests).
        Will use the <b>source</b> field to overwrite the contracts source at a given
        address.</td>
      <td style="text-align:left">N</td>
    </tr>
  </tbody>
</table>

**Example**:

The example below is an [Unlock Protocol](https://unlock-protocol.com/) transaction with the following payload:

```text
{
	"network_id": "1",
	"block_number": 9079267,
	"transaction_index": 5,
	"from": "0xc9E094Deb826b00D10af0aB3D2A62d712e89F67A",
	"input": "0xf6e4641f000000000000000000000000bbaac64b4e4499aa40db238faa8ac00bac50811b",
	"to": "0xb0114bbdce17e0af91b2be32916a1e236cf6034f",
	"gas": 10000000,
	"gas_price": 0,
	"value": 0
}
```

**Response**:

[example-response.json](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4a4d2e4e-794f-4dae-895a-ef620ab76be9/example-response.json)

**Example 2**:

This example shows usage with state objects and contract sources:

```text
{
    "network_id": "42",
    "block_number": null,
    "transaction_index": null,
    "from": "0x0000000000000000000000000000000000000000",
    "input": "0xa41368620000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000563616f6f6f000000000000000000000000000000000000000000000000000000",
    "to": "0x2520c9bfe8d761ba955961e53602dd5c81cea1c5",
    "gas": 1000000,
    "gas_price": "0", 
    "value": 0,
    "save": true,
    "source": "api",
    "state_objects": {
        "0x2520c9bfe8d761ba955961e53602dd5c81cea1c5": {
            "balance": "5000000000",
						"code": "0x",
            "storage": {
                "0x2520c9bfe8d761ba955961e53602dd5c81cea1c52520c9bfe8d761ba95599559": "0x0000000000000000000000000000000000000000000000000000000000000001"
            }
        }
    },
    "contracts": [
        {
            "contractName": "Adoption",
            "source": "pragma solidity ^0.4.17;\\n\\ncontract Adoption {\\n    address[16] public adopters;\\n\\n    function adopt(uint petId) public returns (uint) {\\n        require(petId >= 0 && petId <= 15);\\n\\n        adopters[petId] = msg.sender;\\n\\n        return petId;\\n    }\\n\\n    function getAdopters() public view returns (address[16]) {\\n        return adopters;\\n    }\\n}",
            "sourcePath": "/Users/abencic/Code/Ethereum/pet-shop-tutorial/contracts/Adoption.sol",
            "compiler": {
                "name": "solc",
                "version": "0.4.24+commit.e67f0147.Emscripten.clang"
            },
            "networks": {
                "42": {
                    "events": {},
                    "links": {},
                    "address": "0x7b01b00018c3660dca1d1ed53450e4045c10f94e",
                    "transactionHash": "0x95771f266658055ebc97871d8e177b61b1cb40850cd17f71f6615e41bc43bb7f"
                }
            }
        },
        {
            "contractName": "Migrations",
            "source": "pragma solidity ^0.4.24;\\n\\ncontract Migrations {\\n  address public owner;\\n  uint public last_completed_migration;\\n\\n  modifier restricted() {\\n    if (msg.sender == owner) _;\\n  }\\n\\n  constructor() public {\\n    owner = msg.sender;\\n  }\\n\\n  function setCompleted(uint completed) public restricted {\\n    last_completed_migration = completed;\\n  }\\n\\n  function upgrade(address new_address) public restricted {\\n    Migrations upgraded = Migrations(new_address);\\n    upgraded.setCompleted(last_completed_migration);\\n  }\\n}\\n",
            "sourcePath": "/Users/abencic/Code/Ethereum/pet-shop-tutorial/contracts/Migrations.sol",
            "compiler": {
                "name": "solc",
                "version": "0.4.24+commit.e67f0147.Emscripten.clang"
            },
            "networks": {
                "42": {
                    "events": {},
                    "links": {},
                    "address": "0x81941e4f12e6c7f770ebb8ebd01a7932f968c6cf",
                    "transactionHash": "0x84a8e3ad8a53b0f666d1edcf7a260e7088e66acec6a2246e0a6b7956aada2b2b"
                }
            }
        }
    ]
}
```

