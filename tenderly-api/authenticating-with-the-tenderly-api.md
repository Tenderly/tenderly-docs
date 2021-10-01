# Authenticating with the Tenderly API

## Using a generated Access Token

### Making a new Access Token

If you want to generate a new Access Token you can do it by making the following request:

**Link**: `https://api.tenderly.co/api/v1/user/token`

**Request Type**: `POST`

**Payload**:

```text
{
	"name": "Access Token - Prod"
}
```

### Generating an Access Token through the UI

To get your Access Token go to the **Account &gt; Authorization** part of your Tenderly dashboard \([link](https://dashboard.tenderly.co/account/authorization)\) and click on **Generate Access Token**.

### Authenticating with the Access Token

When making API requests add the `X-Access-Key` header with the value `{{token}}`.

### Revoking an existing Access Token

**Link**: `https://api.tenderly.co/api/v1/user/token/{{token}}`

**Request Type**: `DELETE`

**Payload**: No Payload

## Authentication

In all of the examples, we assume that `access_key` variable contains the Access Token for simplicity.

```text
access_key=xxxxxxxxxxxxxxxxxxxxx
```

