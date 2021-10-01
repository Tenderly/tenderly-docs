# Synthetix API

## Requirements

* \[X\] [Alerting API](alerting-api.md)
* \[X\] [Smart Contract Management API](smart-contract-management-api.md)

## API Authentication

Authenticating with the Tenderly API can be done in two ways:

### 1. Using the Bearer Token

{% hint style="warning" %}
This is the simpler method, but not the preferred method. Bearer tokens cannot be revoked and expire after 30 days.
{% endhint %}

To get your Bearer token go to the **Account &gt; Authorization** part of your Tenderly dashboard \([link](https://dashboard.tenderly.dev/account/authorization)\).

When making API requests add the **`Authorization`** header with the value `Bearer {{token}}`.

### 2. Using a generated Access Token

#### Making a new Access Token

If you want to generate a new Access Token you can do it by making the following request:

**Link**: `https://api.tenderly.dev/api/v1/user/token`

**Request Type**: `POST`

**Payload**:

```text
{
	"name": "Synthetix Access Token - Prod"
}
```

#### Authenticating with the Access Token

When making API requests add the `x-access-key` header with the value `{{token}}`.

#### Revoking an existing Access Token

**Link**: `https://api.tenderly.dev/api/v1/user/token/{{token}}`

**Request Type**: `DELETE`

**Payload**: No Payload

### Authentication

In the following examples, we assume that JWT bearer token is used for simplicity.

```text
JWT=xxxxxxxxxxxxxxxxxxxxx
```

### Account ID

For calls operating over a specific account, which accounts for most of them, an account ID should be provided in the API url.

```text
ACCOUNT_ID=007
```

Optionally, if all the API calls are made on behalf of the account authenticated with the provided `JWT`, a "magic" `me`value can be used instead. Behind the scenes, `me` value is replaced with the account ID inside the `JWT`.

The examples in the documentation will use the `me` shorthand by default.

### Project Slug

As all Tenderly resources are grouped inside of Projects, and a project slug must be provided in order to manage them.

You can find the project slug by calling the Project List endpoint.

```text
curl -X GET '<https://api.tenderly.dev/api/v1/account/me/projects?withShared=true>' \\
--header "Authorization: Bearer ${JWT}"
```

## Contract Management

### Adding an Etherscan verified Smart Contract

```text
PROJECT_SLUG=project-x

curl -X POST "<https://api.tenderly.dev/api/v1/account/me/project/${PROJECT_SLUG}/address>" \\
--header "Content-Type: application/json" \\
--header "Authorization: Bearer ${JWT}" \\
--data-raw '{
	"network_id": "42",
	"address": "0x404469525f6Ab4023Ce829D8F627d424D3986675"
}'
```

## Alerting

### Alert List

```text
curl -X GET "<https://api.tenderly.dev/api/v1/account/me/project/${PROJECT_SLUG}/alerts>" \\
--header "Content-Type: application/json" \\
--header "Authorization: Bearer ${JWT}"
```

### Alert Create

To see all the available expressions, see **Appendix 1** below. To get a list of available delivery channels, see **Delivery Channel List** below as well.

```text
curl -X POST "<https://api.tenderly.dev/api/v1/account/me/project/${PROJECT_SLUG}/alert>" \\
--header "Content-Type: application/json" \\
--header "Authorization: Bearer ${JWT}" \\
--data-raw '{
    "name": "Alert name",
    "description": "This describes the alert",
    "enabled": true,
    "expressions": [
        {
            "type": "method_call",
            "expression": {
                "line_number": 222,
                "call_position": "any"
            }
        },
        {
            "type": "whitelisted_caller_addresses",
            "expression": {
                "addresses": [
                    "0x6b9ef02657339310e28a7a9d4b5f25f7c1f68d61",
                    "0x904ef6ff8e82478c5604d99884eb9bcd7f73cc36"
                ]
            }
        }
    ],
    "delivery_channels": [
        {
            "id": "10159dbf-278e-4f4a-954d-d299c3ddc220",
            "enabled": true
        },
        {
            "id": "4d09b816-e817-4b14-aa00-2aa8022ef5a8",
            "enabled": false
        }
    ]
}'
```

### Delivery Channel List

```text
curl -X GET "<https://api.tenderly.dev/api/v1/account/me/delivery-channels>" \\
	--header "Authorization: Bearer ${JWT}"
```

### Alert Delete

```text
curl -X DELETE "<https://api.tenderly.dev/api/v1/account/me/project/${PROJECT_ID}/alert/${ALERT_ID}>" \\
--header "Content-Type: application/json" \\
--header "Authorization: Bearer ${JWT}"
```

## Appendix 1: Alert Expressions

### Address

```text
{
	"type": "contract_address",
	"expression": {
		"address": "0x6b9ef02657339310e28a7a9d4b5f25f7c1f68d61",
		"transaction_type": "direct"
	}
}
```

The `transaction_type` field is optional or has either the value `direct` or `internal`.

### Network

```text
{
	"type": "network",
	"expression": {
	  "network_id": "42"
	}
}
```

### Transaction Status

```text
{
	"type": "tx_status",
	"expression": {
		"transaction_success": true
	} 
}
```

The `transaction_success` field is optional or has either the value true or false. If not provided it will match any transaction.

### Method Call

```text
{
	"type": "method_call",
	"expression": {
		"line_number": 123,
		"call_position": "any"
	}
}
```

The `line_number` represents the line on which the function was defined. In the future this will be switched for the function's signature.

The `call_position` field can have one of the following values: `first`, `last` or `any`.

### Whitelisted caller address

```text
{
	"type": "whitelisted_caller_addresses",
	"expression": {
		"addresses": [
			"0x6b9ef02657339310e28a7a9d4b5f25f7c1f68d61"
		]
	}
}
```

### Blacklisted caller address

```text
{
	"type": "blacklisted_caller_addresses",
	"expression": {
		"addresses": [
			"0x6b9ef02657339310e28a7a9d4b5f25f7c1f68d61"
		]
	}
}
```

### Emitted Log

#### Basic emitted log expression

```text
{
	"type": "emitted_log",
	"expression": {
		"address": "0x6b9ef02657339310e28a7a9d4b5f25f7c1f68d61",
		"event_name": "Transfer",
		"event_id": "0x241ea03ca20251805084d27d4440371c34a0b85ff108f6bb5611248f73818b80"
	}
}
```

#### Log prototype expression

```text
{
	"type": "emitted_log",
	"expression": {
		"address": "0x6b9ef02657339310e28a7a9d4b5f25f7c1f68d61",
		"event_name": "Transfer",
		"event_id": "0x241ea03ca20251805084d27d4440371c34a0b85ff108f6bb5611248f73818b80",
    "match_any": true,
		"match_non_project_contracts": true
	}
}
```

By passing the `match_any` property you define it is not important that the log was emitted from the `address`, but from any of the contracts inside of the project.

Alternatively, by passing `match_non_project_contracts` as `true` with `match_any`, you define it is not important that the log was emitted from any of the contracts inside of the project.

#### Conditional parameter expression

```text
{
	"type": "emitted_log",
	"expression": {
		"address": "0x6b9ef02657339310e28a7a9d4b5f25f7c1f68d61",
		"event_name": "Transfer",
		"event_id": "0x241ea03ca20251805084d27d4440371c34a0b85ff108f6bb5611248f73818b80",
		"parameter_conditions": [
        {
            "parameter_name": "wad",
            "parameter_type": "uint",
            "operator": ">=",
            "comparison_value": "1000"
        }
    ]
	}
}
```

The `operator` property can be one of `>`, `>=`, `<`, `<=`, `==`, `!=`.

The `comparison_value` property has different formats for different types:

* `int`, `uint`: Passed in as a string due to the possible word size
* `bool`: Passed in as boolean value
* `address`, `string`, `byte`: Passed in as a string

{% hint style="info" %}
Arrays are supported as well, but we didn't want to overcomplicate the example. If you have a use-case for it we will add it to the documentation.
{% endhint %}

### State Change

{% hint style="info" %}
The `match_any`, `match_non_project_contracts` and `parameter_type` properties [work the same like](https://www.notion.so/Synthetix-API-Documentation-982cc9ab45724dcda6ad8b4f70247f10) in the `emitted_log` expression.
{% endhint %}

#### Check if a state variable

```text
{
	"type": "state_change",
	"expression": {
		"address": "0x6b9ef02657339310e28a7a9d4b5f25f7c1f68d61",
		"parameter_conditions": [
        {
            "parameter_name": "pause",
            "parameter_type": "bool",
            "compare_change": true
        }
    ]
	}
}
```

#### Check if a state variable went over/under a threshold

```text
{
	"type": "state_change",
	"expression": {
		"address": "0x6b9ef02657339310e28a7a9d4b5f25f7c1f68d61",
		"parameter_conditions": [
        {
            "parameter_name": "number_of_loans",
            "parameter_type": "uint",
            "compare_threshold": true,
            "comparison_value": "1000",
            "operator": ">"
        }
    ]
	}
}
```

The `operator` property changes the nature of the check:

* `>`: Check if the new value went over the threshold
* `<`: Check if the new value went under the threshold
* `==`: Check if the value went over or under the threshold

{% hint style="info" %}
The threshold check will occur **only** if the threshold was crossed inside the transaction.
{% endhint %}

#### Check if a state variable was changed by a certain percent

```text
{
	"type": "state_change",
	"expression": {
		"address": "0x6b9ef02657339310e28a7a9d4b5f25f7c1f68d61",
		"parameter_conditions": [
        {
            "parameter_name": "available_funds",
            "parameter_type": "uint",
            "compare_percentage": true,
            "comparison_value": "5",
            "operator": ">="
        }
    ]
	}
}
```

The `operator` property changes the nature of the check:

* `>=`: Check if the new value has increased by `comparison_value` percent
* `<=`: Check if the new value has decreased by `comparison_value` percent

#### Check if a state variable is a certain value

This works exactly the same like the **Conditional parameter expression**.

### ETH Balance

```text
{
	"type": "eth_balance",
	"expression": {
		"address": "0x6b9ef02657339310e28a7a9d4b5f25f7c1f68d61",
		"threshold": "1000"
	}
}
```

The `threshold` is the amount of **wei** under which this expression will match.

{% hint style="info" %}
The threshold check will occur **only** if the threshold was crossed inside the transaction.
{% endhint %}

