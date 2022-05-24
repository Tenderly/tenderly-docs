# Triggers

A **trigger** determines on which event or by which schedule your function will be executed. Action trigger is configured in `tenderly.yaml`, if you haven't already, see the [**configuration**](configuration.md). Also, there is an option to configure a trigger through the Dashboard UI.

If the action has just trigger type, it will not run automatically, but you can still use manual triggering. Here is an example of a trigger with just a type:

```yaml
trigger:
  type: block
```

The trigger also defines the event type for your action, so `block` trigger will result in your function getting `BlockEvent`. [**Take a look at our API**](https://github.com/Tenderly/tenderly-actions/blob/main/packages/actions/src/actions.ts) to better understand what each event type has (or log event to console, use manual trigger and check out the output).

## Block

Block trigger will run your action when a block is mined on a configured network.

```yaml
trigger:
  type: block
  block:
    # This action will run when a block is mined on the network with chain id 1.
    network: 1
    # This action will run on every 100th block, eg. 100th, 200th, ...
    blocks: 100
```

You can also listen to blocks on multiple networks with the same trigger.

```yaml
trigger:
  type: block
  block:
    network:
    - 1
    - 42
    blocks: 100
```

If you want to configure a block trigger through the UI, you can do it by going to the Edit Action -> Trigger section.

![Set up a block trigger configuration through the UI](<../.gitbook/assets/image (80) (1).png>)

## Transaction

Transaction trigger consists of `status` and `filters`.

The status field defines at what stage you are listening for transactions. Supported stages are:

* `mined` As soon as the transaction has been mined.
* `confirmed10` Exactly 10 blocks have been mined after block which contains a transaction.
* more coming soon :tada:

Filters field defines what properties transaction must have for your action to run. Filters is a list and if ANY of the filters is matched, your action will run.&#x20;

{% hint style="info" %}
If multiple filters are matched, your actions will still run just once.
{% endhint %}

Within a single filter AND applies, so the transaction must match ALL fields. Most fields can have value or be a list of values, and if list, OR applies so transaction must match ANY value in the list for a given field.&#x20;

```yaml
trigger:
  type: transaction
  transaction:
    # This trigger will listen to both mined and confirmed10 streams of transactions.
    # If you are setting just one, you don't need a list - "status: mined".
    status:
      - mined
      - confirmed10
    # This trigger has two filters and action will run if the transaction matches
    # any of them.
    filters:
        # Transaction must be from the network with chain id 1, which is a mainnet.
      - network: 1
        # Transaction must fail.
        status: fail
        # Transaction must be sent to this address.
        to: 0x2364259ACD20Bd2A8dEfDc628f4099302449fd62
        # Transaction must be sent from this address.
        from: 0xDB638EB2d460CE77bDE8a564b7cEd8b43526BbE1
        
        # Or with more possible values.

        # Transaction must be from either mainnet (1) or kovan (42)
      - network:
          - 1
          - 42
        # Transaction must fail or succeed. This is just an example, in practice this
        # is equivalent to not setting the status field at all.
        status:
          - fail
          - success
        # Transaction must be sent to either of these addresses.
        to:
          - 0x885f70E51e7203c0aBf656c10fde2c4194879d70
          - 0xF215d4Aae591602c9abfbabD0db18DD165ad9288
        # Transaction must be sent from either of these addresses.
        from:
          - 0xC2E52b2697AC97457C2B5FB69944B0537698415A
          - 0x1c58F4812B16C405B0A4D069aEB527a61fcac849
```

In the example above you can see that string fields can be represented with either values or a list of values. Int fields are represented as either an object or a list of objects following a specific schema.

```yaml
gte: ? # greater or equal than
lte: ? # less or equal than
ge: ?  # greater than
le: ?  # less than
eq: ?  # equal to
```

```yaml
trigger:
  type: transaction
  transaction:
    status:
      - mined
    filters:
      - network: 1
        # Transaction must have a value greater than 100 wei.
        value:
          gt: 100
        # Transaction must have used less than or equal to 100k gas.
        gasUsed:
          lte: 100000
        # Transaction must have a gas limit greater than or equal to 200k.
        gasLimit:
          gte: 200000
        # Transaction fee must be less than 1M gwei.
        fee:
          lt: 1000000
        
        # Or with more possible values.

      - network: 1
        # Transaction must have a value between 100 and 1000 wei.
        value:
          gt: 100
          lt: 1000
        # Transaction must have used less than or equal to 100k gas OR more than 200k gas.
        gasUsed:
          - lte: 100000
          - gte: 100000
        # Transaction must have a gas limit greater than or equal to 200k OR less than or equal to 100k.
        gasLimit:
          - gte: 200000
          - lte: 100000
        # Transaction fee must be between 1M and 2M, inclusive.
        fee:
          gte: 1000000
          lte: 2000000
```

More advanced transaction filters include function invocation or an event emitted on a contract.

{% hint style="warning" %}
The contract must be added to your project before it can be referenced in your triggers.
{% endhint %}

```yaml
trigger:
  type: transaction
  transaction:
    status:
      - mined
    filters:
      - network: 1
        # Transaction invoked a function...
        function:
          # on contract with this address...
          contract:
            address: 0xC2E52b2697AC97457C2B5FB69944B0537698415A
          # with function name "stake"
          name: stake
        # Transaction emitted an event...
        eventEmitted:
          # coming from this contract...
          contract:
            address: 0xC2E52b2697AC97457C2B5FB69944B0537698415A
          # with name "Staked"
          name: Staked
        # Or you can filter for raw logs without event decoding
        logEmitted:
          # transaction must product log with topics having this array as prefix,
          # useful when you do not have a contract
          startsWith:
            - 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
            - 0x0000000000000000000000000000000000000000000000000000000000000000

      # Or written in a more compact way

      - network: 1
        # If put at the top, contract will apply to all fields
        # that need it but don't have it.
        contract:
          address: 0xC2E52b2697AC97457C2B5FB69944B0537698415A
        function:
          name: stake
        eventEmitted:
          name: Staked

      # Or with multiple values

      - network: 1
        contract:
          address: 0xC2E52b2697AC97457C2B5FB69944B0537698415A
        # Transaction invoked either "stake" or "stakeNew"
        function:
          - name: stake
          - name: stakeNew
        # Transaction emitted either "Staked" from 0xC2E52b2697AC97457C2B5FB69944B0537698415A...
        eventEmitted:
          - name: Staked
          - contract:
              address: 0xF215d4Aae591602c9abfbabD0db18DD165ad9288
            # or "StakedNew" from 0xF215d4Aae591602c9abfbabD0db18DD165ad9288
            name: StakedNew
        # Or you can filter for raw logs without event decoding
        logEmitted:
          - startsWith:
              - 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
              - 0x0000000000000000000000000000000000000000000000000000000000000000
          - startsWith:
              - 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
              - 0x1111111111111111111111111111111111111111111111111111111111111111
        
        
```

{% hint style="info" %}
The transaction trigger can be configured through the `tenderly.yaml` only.
{% endhint %}

## Webhook

Webhook lets you trigger an action with a `POST` request.

{% hint style="success" %}
If you don't want to schedule your action and just want to run when needed with a custom payload, you can set the trigger type to webhook and use a manual trigger.
{% endhint %}

You can decide if the request should be authenticated or not. If it should be authenticated you must make a request with a valid Tenderly token that can access this action's project.

```yaml
trigger:
  type: webhook
  webhook:
    authenticated: true
```

You can trigger this action with a curl.

```bash
curl -X POST -H "x-access-key: $TENDERLY_TOKEN" -H "Content-Type: application/json" \
https://api.tenderly.co/api/v1/actions/$ACTION_UUID/webhook \
-d '{"dataKey": "dataValue"}'
```

{% hint style="info" %}
You can get this curl generated for your action when you open action in the dashboard.
{% endhint %}

For non-authenticated webhook, you don't have to pass `x-access-key` header.

You can access the body from the request in runtime through WebhookEvent. In this example, `webhookEvent.payload.dataKey` will have value "dataValue".

{% hint style="warning" %}
The payload must be valid JSON and the webhook endpoint will respond with 200 and `{}` if action was triggered successfully.
{% endhint %}

If you want to configure the webhook trigger through the UI, you can do it by going to the Edit Action -> Trigger section.

![Set up the webhook trigger configuration through the UI](<../.gitbook/assets/image (85).png>)

## Periodic

A periodic trigger means your action will be invoked on a fixed schedule.&#x20;

```yaml
# Runs every 5 min: 00:00, 00:05, 00:10...
trigger:
  type: periodic
  periodic:
    # Supported values for interval are 
    # {5m, 10m, 15m, 30m, 1h, 3h, 6h, 12h, 1d}
    interval: 5m
```

Supported values for interval scheduling are: `5m`, `10m`, `15m`, `30m`, `1h`, `3h`, `6h`, `12h`, `1d`.

You can also use CRON scheduling. If you haven't worked with CRON, see [https://crontab.guru](https://crontab.guru/).

```yaml
trigger:
  type: periodic
  periodic:
    # At minute 5 past every hour.
    cron: "5 */1 * * *"
```

If you want to configure a periodic trigger through the UI, you can do it by going to the Edit Action -> Trigger section.

![Set up a periodic trigger configuration through the UI](<../.gitbook/assets/image (78).png>)

![Supported values for interval scheduling](<../.gitbook/assets/image (76).png>)

## Alert

An alert trigger means your action will be used as a [**destination for the alert**](../alerts/creating-an-alert/).

```yaml
trigger:
  type: transaction
  transaction: {}
```

A single action can be used as a destination for multiple alerts. In order to connect your alert to the Web3 Action, you can go to the **Alerting Page** > **Single Alert View** and click on the **Edit** button.

![Single alert view](<../.gitbook/assets/image (87).png>)

For the last step - **Destinations**, you will see available Web3 Actions that can be linked to the selected alert.

![Select Alert destination](<../.gitbook/assets/image (74).png>)

If you want to configure an alert trigger through the UI, you can do it by going to the Single Action View and scrolling down to the Trigger Configuration section.

![Set up an alert trigger configuration through the UI](<../.gitbook/assets/image (93).png>)

![List of the trigger configurations](<../.gitbook/assets/image (96).png>)

![Expandable configuration for the trigger](<../.gitbook/assets/image (77).png>)

![Edit your trigger through the modal](<../.gitbook/assets/image (95).png>)
