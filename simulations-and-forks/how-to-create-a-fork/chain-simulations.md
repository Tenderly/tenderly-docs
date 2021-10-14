# Chain Simulations

## API Authentication

You can read more about API authentication here: [Authenticating with the Tenderly API](../../tenderly-api/authenticating-with-the-tenderly-api.md).

## Chained Simulations

{% hint style="info" %}
The rest of this document assumes you have authenticated with one of the two previously mentioned methods.
{% endhint %}

To start off you'll need to get your `account_id` and `project_slug`. To do so, simply navigate to the dashboard and look at the address bar:

![](<../../.gitbook/assets/image (53).png>)

### 1. Creating an environment

After you have that, you need to create an environment where the states will be stored. You can do that by calling the following endpoint:

**Link:** `https://api.tenderly.co/api/v1/account/{{account_id}}/project/{{project_slug}}/fork`

**Request type**: `POST`

**Payload**:

```
{
    "network_id": "1",
		"block_number": 15107216,
    "transaction_index": 1,
}
```

**Payload explanation**:

| Name              | Type   | Description                                                                                                                                         | Mandatory Y/N |
| ----------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| network_id        | string | ID of the network that we want to fork for our environment.                                                                                         | Y             |
| block_number      | number | Block height - if left out the latest block will be used.                                                                                           | N             |
| transaction_index | number | <p>The index of the transaction inside the block. <br><br>Note: This parameter must be omitted or 0 when the block_number property is left out.</p> | N             |

**Response**:

[fork-response.json](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d19cc9a7-d209-4cea-981c-23ea296de78f/fork-response.json)

In the response we notice 2 main entities:

1. `simulation_fork` From this you will need to store the `id` field for simulation use.
2. `root_transaction` This is a transaction that sets the initial balances of unlocked accounts on the created fork. You can store the `id` field for later use, but it is not mandatory.

### 2. The simulations

Now that that's done, we can get to simulating. The forkID parameter is the one we stored from when we created the environment in step 1. To execute simulations we call the following:

**Link**: `https://api.tenderly.co/api/v1/account/{{account_id}}/project/{{project_slug}}/fork/{{forkID}}/simulate`

**Request type**: `POST`

**Payload**:

```
{
    "from": "0x1E739B75473DF4DaD24Ea68d14a78C093aFe598E",
    "to": "0x8ad82450cb3c8bac5b4357b3c2a2a249212b84cd",
    "input": "0xef690cc0",
    "gas": 8522744,
    "gas_price": "0",
    "value": 0,
    "save": true,
    "root": "55665ad2-f3fa-4768-83a6-c48cc8f74a21"
}
```

**Payload explanation**:

| Name            | Type    | Description                                                                                                                                                                                                     | Mandatory Y/N |
| --------------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| from            | string  | The originating address for the simulated transaction.                                                                                                                                                          | Y             |
| to              | string  | The destination address for the simulated transaction.                                                                                                                                                          | Y             |
| input           | string  | ABI encoded input for the transaction.                                                                                                                                                                          | Y             |
| gas             | number  | The gas limit for the transaction.                                                                                                                                                                              | Y             |
| gas_price       | string  | The gas price for the transaction.                                                                                                                                                                              | N             |
| value           | string  | The ETH value sent in the transaction.                                                                                                                                                                          | N             |
| simulation_type | string  | Either _full_ or _quick - full_ simulations use the contracts source code to generate a full trace, while the _quick_ simulation will only use the contracts bytecode. If omitted, the default value is _full_. | N             |
| save            | boolean | Whether or not to save this simulation for later inspection.                                                                                                                                                    | N             |
| root            | string  | ID of the previous transaction in the chain. If omitted, will behave like a regular simulation.                                                                                                                 | N             |

**Response:**

[simulate-fork-example.json](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/37971b98-c49c-4777-8ff2-871b502144a6/simulate-fork-example.json)

In order to chain transaction simulations simply call the above endpoint and store the returned id somewhere (`id` of the `simulation` entity in the response)

### Extras

#### Verifying contracts deployed to a fork

When you deploy a contract as part of a fork, you can verify it with Tenderly, so you can use all of the tooling for the newly deployed contract.

**Link**: `https://api.tenderly.co/api/v1/account/{{accountID}}/project/{{projectID}}/fork/{{forkID}}/verify`

**Request type**: `POST`

**Payload**:

```
{
    "contracts": [
        {
            "contractName": "Greeter",
            "source": "contract Greeting...",
            "sourcePath": "contracts/Greeter.sol",
            "compiler": {
                "name": "solc",
                "version": "0.6.8"
            },
            "networks": {
                "6a3405b1-aa89-4571-9b70-e6a880654b48": {
                    "address": "0xBd770416a3345F91E4B34576cb804a576fa48EB1"
                }
            }
        },
        {
            "name": "console",
            "source": "...",
            "sourcePath": "@nomiclabs/buidler/console.sol",
            "compiler": {
                "name": "solc",
                "version": "0.6.8"
            }
        }
    ],
    "config": {
        "optimizations_used": true,
        "optimizations_count": 200,
        "evm_version": "istanbul"
    },
    "root": "e8f019bf-9d79-4fe7-b094-9fd33ec67ac1"
}
```

#### Fetching fork transactions

When you deploy a contract as part of a fork, you can verify it with Tenderly, so you can use all of the tooling for the newly deployed contract.

**Link**: `https://api.tenderly.co/api/v1/account/{{accountID}}/project/{{projectID}}/fork/{{forkID}}/transactions?page1&perPage20`

**Request type**: `GET`

**Payload**: N/A
