# Triggers

A **trigger** determines on which event or by which schedule your function will be executed. 

Trigger also defines the event type for your action, so `block` trigger will get `BlockEvent`. 

[**Take a look at our API**](https://github.com/Tenderly/tenderly-actions/blob/main/packages/tenderly-actions/src/actions.ts) to better understand what each event type has.



Action trigger is configured in `tenderly.yaml`:

```
actions:
  your-project-name:
    runtime: v1
    sources: actions
    specs:
      action-name:
        description: Something something something.
        function: src/block:blockNotifierFn
				trigger:
           type: periodic
           periodic: {...}
```

### Periodic

Periodic trigger means your action will be invoked on a fixed schedule. Here are a few examples:

```
# Runs every 5 min: 00:00, 00:05, 00:10, ...
trigger:
  type: periodic
  periodic:
	  interval: 5m # {"5m", "10m", "15m", "30m", "1h", "3h", "6h", "12h", "1d"}

# Or you can use cron
trigger:
  type: periodic
  periodic:
    cron: "*/5 * * * *"  # https://crontab.guru/
```

### Webhook

Webhook lets you trigger an action with a `POST` request. You can decide if the request should be authenticated or not. If it should be authenticated you must make a request with a valid Tenderly token that can access this action's project.

```
trigger:
  type: webhook
  webhook:
    authenticated: true
```

To trigger an action, get the UUID for your action from your dashboard, and make the following `POST` request:

```
curl -X POST -H "x-access-key: $TENDERLY_TOKEN" -H "Content-Type: application/jason" https://api.tenderly.co/api/v1/actions/$ACTION_ID/webhook -d '{
   "myData": "myValue"
}'
```

You can access the body from the request through the event `webhookEvent.payload.myData`.

### Block

Block lets you trigger actions as blocks are mined on the network:

```
trigger:
  type: block
  block:
    network: 1  # mainnet
    blocks: 100

# or you can specify multiple networks
trigger:
  type: block
  block:
    network:
      - 1
      - 3
    blocks: 100
```

### Transaction

```
trigger:
  type: transaction
  transaction:
    status:  # currently supported is only mined or confirmed10
      - mined
      - confirmed10
    filters:  # if any filter is matched, action will be triggered
      # within single filter, all fields are AND, so this will trigger if
      # network is mainnet AND status is failed
      - network: 1
        status: failed
        to: 0x8f369ae35bce72a50f1188b96d516fab425511c9
      # but within single field, values are OR, so this will trigger if
      # to is any of specified values AND network is mainnet AND status failed
      - network: 1
        status: fail  {succe
        to:
          - 0x8f369ae35bce72a50f1188b96d516fab425511c9
          - 0x2463bebe23d1b82c28d4ba8e2852d40eedde8f8b
```

String fields that you can combine in your filter are `network`, `status`, `to` and `from`. For each string field you can either specify a value or a list of values. To filter for specific gas usage:

```
filters:
  - gasUsed:
      # greater or equal than
      gte: 100000
      # less or equal than
      lte: ...
      # greater than
      ge: ...
      # less than
      le: ...
      # equal to
      eq: ...
# you can also OR multiple conditions
filters:
  - gasUsed:  # x >= 10000 || x <= 100
      - gte: 100000
      - lte: 100      
```

You can combine the Int fields in your filters, which are - `value`, `gasUsed`, `gasLimit`, `fee`.

More advanced transaction filters include function invocation or an event emitted on a contract \[more coming soon :tada:].

Keep in mind that the contract must be added to your project before it can be referenced in your triggers.

```
filters:
  - function:
      contract:
        address: 0x8f369ae35bce72a50f1188b96d516fab425511c9
      name: stake
  - eventEmitted:
      contract:
        address: 0x8f369ae35bce72a50f1188b96d516fab425511c9
      name: Staked
# if you'd like to AND this, you can write it in a more compact way
filters:
    # contract can be specified for filter and will apply wherever contract is
    # needed but not specified
  - contract:
      address: 0x8f369ae35bce72a50f1188b96d516fab425511c9
    function:
      name: stake
    eventEmitted:
      name: Staked
```
