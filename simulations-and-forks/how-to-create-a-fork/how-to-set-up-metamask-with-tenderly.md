# How to set up Metamask with Tenderly

## API Authentication

You can read more about API authentication here: [Authenticating with the Tenderly API](../../tenderly-api/authenticating-with-the-tenderly-api.md).

{% hint style="info" %}
The rest of this document assumes you have authenticated with one of the two previously mentioned methods.
{% endhint %}

To start off you'll need to get your `account_id` and `project_slug`. To do so, simply navigate to the dashboard and look at the address bar:

![](<../../.gitbook/assets/image (51).png>)

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
		"initial_balance": 10000
}
```

**Payload explanation:**

| Name              | Type   | Description                                                                                                                                         | Mandatory Y/N |
| ----------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| network_id        | string | ID of the network that we want to fork for our environment.                                                                                         | Y             |
| block_number      | number | Block height - if left out the latest block will be used.                                                                                           | N             |
| transaction_index | number | <p>The index of the transaction inside the block. <br><br>Note: This parameter must be omitted or 0 when the block_number property is left out.</p> | N             |
| initial_balance   | number | Amount in ETH, will set the balance of all generated accounts to provided value. Defaults to 100.                                                   | N             |

**Response**:

*   Fork response

    ```
    {
      "simulation_fork": {
        "id": "0b575d7d-f9bb-456f-9ac1-fe0a66a267bd",
        "project_id": "111ee6b7-0dd3-41c0-a660-e503aac36805",
        "network_id": "1",
        "block_number": 11632562,
        "transaction_index": 0,
        "chain_config": "{\\"type\\":\\"ethereum\\",\\"chainId\\":1,\\"homesteadBlock\\":1150000,\\"daoForkBlock\\":1920000,\\"daoForkSupport\\":true,\\"eip150Block\\":2463000,\\"eip150Hash\\":\\"0x2086799aeebeae135c246c65021c82b4e15a2c451340993aacfd2751886514f0\\",\\"eip155Block\\":2675000,\\"eip158Block\\":2675000,\\"byzantiumBlock\\":4370000,\\"constantinopleBlock\\":7280000,\\"petersburgBlock\\":7280000,\\"istanbulBlock\\":9069000}",
        "created_at": "2021-01-11T09:37:48.275896+01:00",
        "accounts": {
          "0x1eF75EB422BAcB3c911e58888eF1a6eC805fC866": "0xbb2bd81f06cb1fbbc518d11b1277d7bca8d7eaf711f316513c53859bfcef39f5",
          "0x297c7Fa1494d51981512E288517D5c49A7Af29Fa": "0x594d146720eb2300b67533af3922461b308bbf9e6a4e91eadc1e71d2c9936e8d",
          "0x403a22DC1614502b293AA17d1aC3d820DF18EE8f": "0x5f4c700291b230d659f82fd9e4f46c1298025a1effec7c016943663630fa36fb",
          "0x41b69ABCA5F0F11AC49353fBc6D7935c1dE252eb": "0x4d3271b791a6cf3556804bfad7b36e5cda1326518072203e6165a69439a48154",
          "0x5916faa12b90B3F408E968E562E831C1F37eFC76": "0x885270ee9984fce4244bad897ad861351eca96b0c0de7a472525f3e99de30760",
          "0x6E5E7CD1a4f99c44290Ec12f865Ec2b3aAB6e65B": "0xbdc20122dff94e4e80da344bbf707c0c5d8dca4506b4695c93a8a668785b6772",
          "0x7EcdA01391C4124170CdC9D4a169678411972F63": "0x08ea3efee1344c59ed0c7343e26feabfb141e1ff7b3ccc4e8d1d6b190fda6576",
          "0x9751A495A7dcdAeaDb94169838d74E98A3fCE701": "0x3926e1f3ad2d7333c53b69146789f3773acea890f558795eb21c99a2e36c5c4d",
          "0xF1684E00a19B8A60CAd4bed3bFf6cD39A110366A": "0x3d9e6f1f4c0b9f12663813a75a662cf699289eb8ae2711c429a19742bd608c49",
          "0xbBddEFCa8F48Ff612182Ce1156677e447D828b98": "0x7f349f6afc77fd7c23f94b2130e6094ba0730fd08114716a95929c20e87a17ce"
        }
      },
      "root_transaction": {
        "id": "c9844790-f223-4879-bff1-7442b2fab5cc",
        "project_id": "111ee6b7-0dd3-41c0-a660-e503aac36805",
        "fork_id": "0b575d7d-f9bb-456f-9ac1-fe0a66a267bd",
        "hash": "0xbb70f34d5521fe5f1c4541fc0ef7326131ce1a4c67aa2e446264706d16205e66",
        "state_objects": [
          {
            "address": "0x1eF75EB422BAcB3c911e58888eF1a6eC805fC866",
            "data": {
              "balance": "BWvHXi1jEAAA"
            }
          },
          {
            "address": "0x41b69ABCA5F0F11AC49353fBc6D7935c1dE252eb",
            "data": {
              "balance": "BWvHXi1jEAAA"
            }
          },
          {
            "address": "0x6E5E7CD1a4f99c44290Ec12f865Ec2b3aAB6e65B",
            "data": {
              "balance": "BWvHXi1jEAAA"
            }
          },
          {
            "address": "0xbBddEFCa8F48Ff612182Ce1156677e447D828b98",
            "data": {
              "balance": "BWvHXi1jEAAA"
            }
          },
          {
            "address": "0xF1684E00a19B8A60CAd4bed3bFf6cD39A110366A",
            "data": {
              "balance": "BWvHXi1jEAAA"
            }
          },
          {
            "address": "0x7EcdA01391C4124170CdC9D4a169678411972F63",
            "data": {
              "balance": "BWvHXi1jEAAA"
            }
          },
          {
            "address": "0x403a22DC1614502b293AA17d1aC3d820DF18EE8f",
            "data": {
              "balance": "BWvHXi1jEAAA"
            }
          },
          {
            "address": "0x9751A495A7dcdAeaDb94169838d74E98A3fCE701",
            "data": {
              "balance": "BWvHXi1jEAAA"
            }
          },
          {
            "address": "0x5916faa12b90B3F408E968E562E831C1F37eFC76",
            "data": {
              "balance": "BWvHXi1jEAAA"
            }
          },
          {
            "address": "0x297c7Fa1494d51981512E288517D5c49A7Af29Fa",
            "data": {
              "balance": "BWvHXi1jEAAA"
            }
          }
        ],
        "network_id": "1",
        "block_number": 11632562,
        "transaction_index": 0,
        "from": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "to": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "input": "",
        "gas": 0,
        "gas_price": "",
        "value": "",
        "status": true,
        "fork_height": 0,
        "block_hash": "0x2c928012593f898360d6be1c538d878efd8684f00430b432cd2a6ae2fa2ecf44",
        "nonce": 0,
        "receipt": {
          "transactionHash": "0xbb70f34d5521fe5f1c4541fc0ef7326131ce1a4c67aa2e446264706d16205e66",
          "transactionIndex": "0x0",
          "blockHash": "0x2c928012593f898360d6be1c538d878efd8684f00430b432cd2a6ae2fa2ecf44",
          "blockNumber": "0xb17fb2",
          "from": "0x0000000000000000000000000000000000000000000000000000000000000000",
          "to": "0x0000000000000000000000000000000000000000000000000000000000000000",
          "cumulativeGasUsed": "0x0",
          "gasUsed": "0x0",
          "contractAddress": null,
          "logs": [],
          "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
          "status": "0x1"
        },
        "parent_id": "",
        "created_at": "2021-01-11T09:37:48.463093+01:00"
      }
    }
    ```

[fork-response.json](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d19cc9a7-d209-4cea-981c-23ea296de78f/fork-response.json)

In the response we notice 2 main entities:

1. `simulation_fork` From this you will need to store the `id` field.
2. `root_transaction` This will not be relevant to the Metamask use case.

### 2. Connecting to Metamask

Next we need to go to the Metamask custom RPC page:

![](<../../.gitbook/assets/image (17).png>)

The RPC URL field is filled with (forkID is the id we stored from step 1):`https://rpc.tenderly.co/fork/{{forkID}}`

The chain ID field will be the one you created the environment with (`network_id` field from step 1)

And that's it!

### 3. Inspecting Transactions

All of the transactions in an environment can be viewed in our debugger by navigating to

`https://dashboard.tenderly.co/{{accountID}}/{{projectID}}/fork/{{forkID}}/simulation/{{transactionID}}`

ForkID is the id from step 1. Transaction ID is returned in every request to the RPC node as the `Head` header, indicating the latest transaction in the environment.

![](<../../.gitbook/assets/image (34).png>)

The RPC endpoint can also be targeted directly with jsonrpc payloads at:

`https://rpc.tenderly.co/fork/{{forkID}}`

### Bonus:

#### Adding balance to accounts:

**Link**:

`https://api.tenderly.co/api/v1/account/{{account_id}}/project/{{projectId}} /fork/{{forkID}}/balance`

**Request type**:

`POST`

**Payload**:

```
{
    "accounts": ["0x3Df2f692132f55b97cc9DA04A1fFFEA82F5d710b"],
		"amount": 1000,
}
```

**Payload explanation:**

| Name     | Type         | Description                                                                          | Mandatory Y/N |
| -------- | ------------ | ------------------------------------------------------------------------------------ | ------------- |
| accounts | string array | Addresses of the accounts we want to add funds to.                                   | Y             |
| amount   | number       | Amount in ETH, will set the balance of all accounts to given value. Defaults to 100. | N             |

This will set the balance for provided accounts to 100 ETH.

#### Transaction history:

**Link:**

`https://api.tenderly.co/api/v1/account/{{account_id}}/project/{{projectId}} /fork/{{forkID}}/transactions?page=1&perPage=20`

**Request type:**

`GET`

**Request explanation:**

| Name    | Type   | Description                         | Mandatory Y/N |
| ------- | ------ | ----------------------------------- | ------------- |
| page    | number | Page to calculate offset.           | N             |
| perPage | number | Count per page to calculate offset. | N             |

**Example response:**

```
{
    "fork_transactions": [
        {
            "id": "a69db85b-caec-47d4-8aa6-b607f65ce279",
            "project_id": "513070f4-8eab-4473-a22f-9c262e44c246",
            "fork_id": "8ca72bcc-b18d-459e-bb22-088c43653fdc",
            "hash": "0x164e0c9a9f12935913e4483866a8dd5f5515db2aa1e263eb1a15914f9d2c66ba",
            "state_objects": [
                {
                    "address": "0x3Df2f692132f55b97cc9DA04A1fFFEA82F5d710b",
                    "data": {
                        "nonce": 2
                    }
                }
            ],
            "network_id": "1",
            "block_number": 11679174,
            "transaction_index": 0,
            "from": "0x3df2f692132f55b97cc9da04a1fffea82f5d710b",
            "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
            "input": "0xd46e8dd67c5d32be8d46e8dd67c5d32be8058bb8eb970870f072445675058bb8eb970870f072445675",
            "gas": 30400,
            "gas_price": "0",
            "value": "0",
            "status": true,
            "fork_height": 3,
            "block_hash": "0xccef08861dc5f9db7d1f7fc5762ef5e444e0716471dafeffc9dab38302a84664",
            "nonce": 1,
            "receipt": {
                "transactionHash": "0x164e0c9a9f12935913e4483866a8dd5f5515db2aa1e263eb1a15914f9d2c66ba",
                "transactionIndex": "0x0",
                "blockHash": "0xccef08861dc5f9db7d1f7fc5762ef5e444e0716471dafeffc9dab38302a84664",
                "blockNumber": "0xb235c6",
                "from": "0x3df2f692132f55b97cc9da04a1fffea82f5d710b",
                "to": "0xd46e8dd67c5d32be8058bb8eb970870f07244567",
                "cumulativeGasUsed": "0x5498",
                "gasUsed": "0x5498",
                "contractAddress": null,
                "logs": [],
                "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
                "status": "0x1"
            },
            "parent_id": "0ff87df5-55b2-4e14-b680-7c192ab6dccf",
            "created_at": "2021-01-18T12:18:18.963892Z"
        }
    ]
}
```
