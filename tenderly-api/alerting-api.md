# Alerting API

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

## Contract Management

### Adding an Etherscan verified Smart Contract

```text
PROJECT_SLUG=project-x

curl -X POST "<https://api.tenderly.co/api/v1/account/me/project/${PROJECT_SLUG}/address>" \\
--header "Content-Type: application/json" \\
--header "X-Access-Key: ${access_key}" \\
--data-raw '{
	"network_id": "42",
	"address": "0x404469525f6Ab4023Ce829D8F627d424D3986675"
}'
```

## Alerting

### Alert List

```text
curl -X GET "<https://api.tenderly.co/api/v1/account/me/project/${PROJECT_SLUG}/alerts>" \\
--header "Content-Type: application/json" \\
--header "X-Access-Key: ${access_key}"
```

### Alert Create

To see all the available expressions, see **Appendix 1**, and to get a list of available delivery channels, see **Delivery Channel List**, both on [this link](synthetix-api.md).

```text
curl -X POST "<https://api.tenderly.co/api/v1/account/me/project/${PROJECT_SLUG}/alert>" \\
--header "Content-Type: application/json" \\
--header "X-Access-Key: ${access_key}" \\
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
curl -X GET "<https://api.tenderly.co/api/v1/account/me/delivery-channels>" \\
--header "X-Access-Key: ${access_key}"
```

### Alert Delete

```text
curl -X DELETE "<https://api.tenderly.co/api/v1/account/me/project/${PROJECT_ID}/alert/${ALERT_ID}>" \\
--header "Content-Type: application/json" \\
--header "X-Access-Key: ${access_key}"
```

### Alert History

```text
curl -X GET "<https://api.tenderly.co/api/v1/account/me/project/${PROJECT_ID}/alert-history?page=1&perPage=20>" \\
--header "Content-Type: application/json" \\
--header "X-Access-Key: ${access_key}"
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

The `transaction_type` field is optional or has either the value `direct`, `source` or `internal`.

### Network

```text
{
	"type": "network",
	"expression": {
	  "network_id": "42"
	}
}
```

### Tag

```text
{
	"type": "tag",
	"expression": {
	  "tag": "my-tag",
		"transaction_type": "direct"
	}
}
```

The `transaction_type` field is optional or has either the value `direct`, `source` or `internal`.

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

### Function params

```text
{
    "type":"function_params",
    "expression":{
      "address":"0xdac17f958d2ee523a2206206994597c13d831ec7", // contract address
      "function_line_number":118, // definition line number of desired function
      "parameter_conditions":[
        {
          "parameter_name":"wad", // function parameter
          "operator":">", 
          "parameter_type":"uint",
          "nested_parameter_type":"",
          "comparison_value":"1"
        }
      ]
    }
}
```

This is all needed data to filter function calling parameter. `wad > 1` \(`<parameter_name>` `<operator><comparison_value>`\)

### Transaction Value

```text
{
	"type": "tx_value",
	"expression": {
		"transaction_value": "1000",
		"operator": ">"
	} 
}
```

The `transaction_value` filed is native `wei` value of transaction and `operator` is anything that is considered a logical operator \( `>`, `>=`, etc.\)

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
    "decode_events": true,
    "match_non_project_contracts": true
	}
}
```

By passing the `match_any` property you define it is not important that the log was emitted from the `address`, but from any of the contracts inside of the project.

Alternatively, by passing `match_non_project_contracts` as `true` with `match_any`, you define it is not important that the log was emitted from any of the contracts inside of the project.

By passing `decode_events` any `bytes` fields will be decoded and sent as UTF-8 strings instead of hex.

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

The `operator` property can be one of `>`, `>=`, `<`, `<=`, `==`, `!=`, `contains`, `notContains` \(for arrays\).

The `comparison_value` property has different formats for different types:

* `int`, `uint`: Passed in as a string due to the possible word size
* `bool`: Passed in as a boolean value
* `address`, `string`, `byte`: Passed in as a string

Arrays are supported as well, but we didn't want to overcomplicate the example. If you have a use case for it we will add it to the documentation.

### State Change

The `match_any`, `match_non_project_contracts` and `parameter_type` properties [work the same](alerting-api.md) as in the `emitted_log` expression.

#### Check if a state variable changed

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

The threshold check will occur **only** if the threshold was crossed inside the transaction.

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

This works exactly the same like the [Conditional parameter expression](alerting-api.md).

### View Function

```text
{
    "type": "view_function",
    "expression": {
        "address": "0x47412bbd86637e15d3de46f1ba3fa2e9d44f808f",
        "input": "0xf2c9ecd8",
        "network_id": "42",
        "parameter_condition": {
            "compare_threshold": true,
            "comparison_value": "200",
            "operator": ">",
            "parameter_type": "uint"
        }
    }
}
```

View function works almost exactly the same as a state change. It however needs some additional parameters:

* `address` - address of the monitored contract
* `network_id` - chain id of the network
* `input` - this is the ABI encoded data used to invoke the view function on the contract

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

The threshold check will occur **only** if the threshold was crossed inside the transaction.

### ERC20 Transfer state and log mismatch

```text
{
	"type": "erc20_transfer_matcher",
	"expression": {
		"address": "0xdac17f958d2ee523a2206206994597c13d831ec7",
		"log_name": "Transfer",
    "balances": "balances"
	}
}
```

The expression will be matched in one of three cases:

* Match if the amount parameter of the Transfer event doesn’t match the changed balances
* Match if the balances changed but there was no Transfer event
* Match if there was a Transfer event but the balances didn’t change

The `log_name` is the name of the event that is fired upon token transfer, `balances` is the name of the `mapping(address ⇒ uint)` property that tracks balances for every address.

### Transaction Error

```text
{
	"type": "tx_error",
	"expression": {
		"addresses_to_ignore": [
        "0xdac17f958d2ee523a2206206994597c13d831ec7",
        "0x0dfb372f34ab40e618b3f0e0d1a646938d086231"
    ]
	}
}
```

The expression will match if a transaction fails, **but not as part of a require or assert**. This can be really useful to check if your transactions are failing with "not enough gas", "not enough ETH to send" or any other unforeseen errors.

You can use the  `addresses_to_ignore` array to ignore certain contracts.

### Transaction Internal Error

```text
{
	"type": "tx_internal_error",
	"expression": {
		"addresses_to_match": [
        "0xdac17f958d2ee523a2206206994597c13d831ec7",
        "0x0dfb372f34ab40e618b3f0e0d1a646938d086231"
    ]
	}
}
```

The expression will match if the top-level transaction is successful, but an internal transaction failed at some point during execution.

You can use the optional  `addresses_to_match` array to only check for failure in certain contracts.

### Maximum time since last action

```text
{
  "type": "no_action",
  "expression": {
    "no_log": {...},
		"no_transaction": {...},
    "check_after_seconds": {{seconds}} // how much to wait for the action
  }
}
```

This expression is quite flexible. You can schedule either the `no_log` or the `no_transaction` check in the future.

You can combine this expression to schedule a check if any other [expression](https://www.notion.so/Alerting-docs-a14b16e80cbb4e3689016501ac97789b) matches

#### No Log

```text
{
  "address": "{{address}}", // address of the contract emitting the log
  "network_id": "{{network_id}}", //network where the emitting contract is
  "event_id": "{{event_id}}" // log signature (topics[0])
  "event_name": "{{event_name}}" // used for display in the notification
}
```

#### No Transaction

```text
{
  "address": "{{address}}",
  "is_from_address": true, // source or the destination of the tx
  "network_id": "{{network_id}}",
  "transaction_success": true // successful/failed transaction
}
```

