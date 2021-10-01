# Account Tokens API

## API Authentication

Authenticating with the Tenderly API can be done in two ways:

### 1. Using the Bearer Token

{% hint style="warning" %}
This is the simpler method, but not the preferred method. Bearer tokens cannot be revoked and expire after 30 days.
{% endhint %}

To get your Bearer token go to the **Account &gt; Authorization** part of your Tenderly dashboard \([link](https://dashboard.tenderly.dev/account/authorization)\).

When making API requests add the **`Authorization`** header with the value `Bearer {{token}}`.

### 2. Using a generated Access Token

#### Authenticating with the Access Token

When making API requests add the `x-access-key` header with the value `{{token}}`.

#### Making a new Access Token

If you want to generate a new Access Token you can do it by making the following request:

**Link**: `https://api.tenderly.co/api/v1/user/token`

**Request Type**: `POST`

**Payload**:

```text
{
	"name": "Token - Prod"
}
```

#### Revoking an existing Access Token

**Link**: `https://api.tenderly.co/api/v1/user/token/{{token}}`

**Request Type**: `DELETE`

**Payload**: No Payload

#### Generating an Access Token through the UI

To get your Access Token go to the **Account &gt; Authorization** part of your Tenderly dashboard \([link](https://dashboard.tenderly.co/account/authorization)\) and click on **Generate Access Token**.

## Account Tokens API

The rest of this document assumes you have authenticated with one of the two previously mentioned methods.

**Link**: `https://api.tenderly.co/api/v1/account/{{accountId}}/token/{{networkId}}/{{accountAddress}}`

**Request Type**: `POST`

**Payload**: No Payload

**Parameters**:

* **accountId**: The ID of the users account. You can just pass in `me` for the user authenticated via the selected authentication method
* **networkId**: The ID of the network which is queries. Use `1` for Mainnet
* **accountAddress**: The address for which the tokens are fetched
* **Example Response:**

  ```text
  {
      "tokens": [
          {
              "address": "0x22c1f6050e56d2876009903609a2cc3fef83b415"
          },
          {
              "address": "0x278dc8dc084863b68d15b29ae8a27f7f7416ba8f"
          },
          {
              "address": "0x4dc3643dbc642b72c158e7f3d2ff232df61cb6ce",
              "token_info": {
                  "network_id": "1",
                  "address": "0x4dc3643dbc642b72c158e7f3d2ff232df61cb6ce",
                  "type": "ERC20",
                  "symbol": "AMB",
                  "name": "Amber Token",
                  "decimals": 18
              }
          },
          {
              "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
              "token_info": {
                  "network_id": "1",
                  "address": "0x6b175474e89094c44da98b954eedeac495271d0f",
                  "type": "ERC20",
                  "symbol": "DAI",
                  "name": "Dai Stablecoin",
                  "decimals": 18
              }
          },
          {
              "address": "0x89d24a6b4ccb1b6faa2625fe562bdd9a23260359",
              "token_info": {
                  "network_id": "1",
                  "address": "0x89d24a6b4ccb1b6faa2625fe562bdd9a23260359",
                  "type": "ERC20",
                  "symbol": "",
                  "name": "",
                  "decimals": 18
              }
          },
          {
              "address": "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48"
          },
          {
              "address": "0xaad5bff48e1534ef1f2f0a4184f5c2e61ac47ec3"
          },
          {
              "address": "0xb0114bbdce17e0af91b2be32916a1e236cf6034f",
              "token_info": {
                  "network_id": "1",
                  "address": "0xb0114bbdce17e0af91b2be32916a1e236cf6034f",
                  "type": "ERC721",
                  "symbol": "",
                  "name": "Unlock Blog Members"
              }
          },
          {
              "address": "0xf1a57ae58253c2b6865ed0861ca0213bca7ab9cb"
          },
          {
              "address": "0xf5b0a3efb8e8e4c201e2a935f110eaaf3ffecb8d",
              "token_info": {
                  "network_id": "1",
                  "address": "0xf5b0a3efb8e8e4c201e2a935f110eaaf3ffecb8d",
                  "type": "ERC721",
                  "symbol": "AXIE",
                  "name": "Axie"
              }
          }
      ]
  }
  ```

