# Transaction

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
