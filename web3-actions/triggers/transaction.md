# Transaction

Transaction trigger consists of `status` and `filters`.

Status field defines at what stage you are listening for transactions. Supported stages are \[more coming soon :tada:]:

* `mined` As soon as transaction has been mined.
* `confirmed10` 10 blocks have been mined after block which contains a transaction.

Filters field defines what properties transaction must have for your action to run. Filters is a list and if ANY of the filters is matched, your action will run. If multiple filters are matched, you actions will still run just once.

Within a single filter AND applies, so transaction must match ALL fields. Most fields can have value or be a list of values, and if list, OR applies so transaction must match ANY value in the list for a given field.&#x20;

```yaml
trigger:
  type: transaction
  transaction:
    # This trigger will listen to both mined and confirmed10 streams of transactions.
    # If your are setting just one, you don't need a list - "status: mined".
      - mined
      - confirmed10
    # This trigger has two filters and action will run if transaction matches
    # any of them.
    filters:
        # Transaction must be from network with chain id 1, which is a mainnet.
      - network: 1
        # Transaction must fail.
        status: fail
        # Transaction must be sent to this address.
        to: 0x2364259ACD20Bd2A8dEfDc628f4099302449fd62
        # Transaction must be sent from this address.
        from: 0xDB638EB2d460CE77bDE8a564b7cEd8b43526BbE1
        
        # Or with more possible values.

        # Transaction must be from either mainnet (1) or kovan (3)
      - network:
          - 1
          - 3
        # Transaction must fail or succeed. This is just an example, in practice this
        # is equivalent to not setting status field at all.
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

In example above you can see that string fields can be represented with either values or list of values. Int fields are represented as either an object or list of objects following a specific schema.

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
      - mined
    filters:
      - network: 1
        # Transaction must have value greater than 100 wei.
        value:
          gt: 100
        # Transaction must have used less than or equal to 100k gas.
        gasUsed:
          lte: 100000
        # Transaction must have gas limit greater than or equal to 200k.
        gasLimit:
          gte: 200000
        # Transaction fee must be less than 1M gwei.
        fee:
          lt: 1000000000
        
        # Or with more possible values.

      - network: 1
        # Transaction must have value between 100 and 1000 wei.
        value:
          gt: 100
          lt: 1000
        # Transaction must have used less than or equal to 100k gas OR more than 200k gas.
        gasUsed:
          - lte: 100000
          - gte: 100000
        # Transaction must have gas limit greater than or equal to 200k OR less than or equal to 100k.
        gasLimit:
          - gte: 200000
          - lte: 100000
        # Transaction fee must be between 1M and 2M, inclusive.
        fee:
          gte: 1000000000
          lte: 2000000
```

More advanced transaction filters include function invocation or an event emitted on a contract \[more coming soon :tada:].

{% hint style="warning" %}
Contract must be added to your project before it can be referenced in your triggers.
{% endhint %}

```yaml
trigger:
  type: transaction
  transaction:
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
```

