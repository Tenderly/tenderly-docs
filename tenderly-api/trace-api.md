# Trace API

## API Authentication

You can read more about API authentication here: [Authenticating with the Tenderly API](authenticating-with-the-tenderly-api.md).

### Account ID

For calls operating over a specific account, which accounts for most of them, an account ID should be provided in the API url.

```text
ACCOUNT_ID=007
```

Optionally, if all the API calls are made on behalf of the account authenticated with the provided Access Token, a "magic" `me` value can be used instead. Behind the scenes, `me` value is replaced with the account ID which is the owner of the Access Token.

The examples in the documentation will use the `me` shorthand by default.

## Fetching a trace

```text
curl -X GET "<https://api.tenderly.co/api/v1/public-contract/${network_id}/trace/${tx_hash}>" \\
--header "Content-Type: application/json" \\
--header "X-Access-Key: ${access_key}"
```

## Fetching a trace with a project scope

```text
curl -X GET "<https://api.tenderly.co/api/v1/account/me/project/${projectSlug}/network/${network_id}/trace/${tx_hash}>" \\
--header "Content-Type: application/json" \\
--header "X-Access-Key: ${access_key}"
```

You can find an [example Uniswap transaction here](https://api.tenderly.co/api/v1/public-contract/1/trace/0x48fb6533194e079c58f2edd26a11c5a56af0ccb678d2b93f80da5b0ce1ec4cd5).

