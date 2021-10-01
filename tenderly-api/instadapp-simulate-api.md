# InstaDapp Simulate API

## API Authentication

Authenticating with the Tenderly API can be done in two ways:

### 1. Using the Bearer Token

{% hint style="warning" %}
This is the simpler method, but not the preferred method. Bearer tokens cannot be revoked and expire after 30 days.
{% endhint %}

To get your Bearer token go to the **Account &gt; Authorization** part of your Tenderly dashboard \([link](https://dashboard.tenderly.dev/account/authorization)\).

When making API requests add the **`Authorization`** header with the value `Bearer {{token}}`.

### 2. Using a generated Access Token

We have already generated an access token for you:

```text
{
    "name": "InstaDApp Access Token - Prod",
    "token": "kVrvihRnEyISbf197tMczh7EMzxKaEpa",
    "created_at": "2020-02-12T16:52:07.53086605Z"
}
```

#### Authenticating with the Access Token

When making API requests add the `x-access-key` header with the value `{{token}}`.

#### Making a new Access Token

If you want to generate a new Access Token you can do it by making the following request:

**Link**: `https://api.tenderly.dev/api/v1/user/token`

**Request Type**: `POST`

**Payload**:

```text
{
	"name": "InstaDApp Access Token - Prod"
}
```

#### Revoking an existing Access Token

**Link**: `https://api.tenderly.dev/api/v1/user/token/{{token}}`

**Request Type**: `DELETE`

**Payload**: No Payload

## Simulate API

The rest of this document assumes you have authenticated with one of the two previously mentioned methods.

Because the Simulate API supports saving simulations, you will need to specify a project when calling the API. The project is determined by the `project_slug` path parameter. You can find the slug for you project in the address bar:

![](../.gitbook/assets/image%20%2859%29.png)

**Link**: \*\*\*\*`https://api.tenderly.dev/api/v1/account/me/project/{{project_slug}}/simulate`

**Request Type**: `POST`

**Payload**:

The simulate payload is similar to the [eth\_call](https://github.com/ethereum/wiki/wiki/json-rpc#eth_call) JSON RPC call.

```text
{
    "network_id": "1",
    "block_number": 15107216,
    "transaction_index": 1,
    "from": "0x0000000000000000000000000000000000000012",
    "to": "0x0000000000000000000000000000000000000000",
    "input": "0x",
    "gas": 10000000,
    "gas_price": 0,
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

