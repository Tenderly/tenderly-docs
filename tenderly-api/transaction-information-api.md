# Transaction Information API

## API Authentication

You can read more about API authentication here: [Authenticating with the Tenderly API](authenticating-with-the-tenderly-api.md).

### Account ID

For calls operating over a specific account, which accounts for most of them, an account ID should be provided in the API url.

```text
ACCOUNT_ID=007
```

Optionally, if all the API calls are made on behalf of the account authenticated with the provided Access Token, a "magic" `me` value can be used instead. Behind the scenes, `me` value is replaced with the account ID which is the owner of the Access Token.

The examples in the documentation will use the `me` shorthand by default.

### Project Slug

As all Tenderly resources are grouped inside of Projects, and a project slug must be provided in order to manage them.

You can find the project slug by calling the Project List endpoint.

```text
curl -X GET '<https://api.tenderly.co/api/v1/account/me/projects?withShared=true>' \\
--header "X-Access-Key: ${access_key}"
```

### Network ID

The network ID is used to pick which network is used when fetching a transaction:

### Network List:

| Network | ID |
| :--- | :--- |
| Mainnet | 1 |
| Ropsten | 3 |
| Rinkeby | 4 |
| Goerli | 5 |
| Kovan | 42 |
| POA | 99 |
| xDai | 100 |
| Matic Testnet V3 | 15001 |
| Binance | 56 |
| Rialto Binance | 97 |

## Transaction Information API

There are two ways to fetch information about a particular transaction:

1. Fetching the transaction with the scope being a project
2. Fetching the transaction with publicly available information

### Fetching a project transaction information

```text
curl -X GET '<https://api.tenderly.co/api/v1/account/me/project/{{projectSlug}>}/network/{{networkID}}/transaction/{{transactionHash}}' \\
--header "X-Access-Key: ${access_key}"
```

{% hint style="info" %}
By using the project as the scope of the transaction tracing, Tenderly will take into account private contracts that were added via the [CLI](https://github.com/tenderly/tenderly-cli#push) or the Contract Management API.
{% endhint %}

### Fetching a public transaction

```text
curl -X GET '<https://api.tenderly.co/api/v1/public-contract/{{networkID}/transaction/{{transcationHash}>}' \\
--header "X-Access-Key: ${access_key}"
```

{% hint style="info" %}
The authorization header is optional.
{% endhint %}

