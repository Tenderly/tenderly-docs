# Transaction

Transaction trigger consists of `status` and `filters`.

Status field defines at what stage you are listening for transactions. Currently supported stages are `mined` and `confirmed10`.

Filters field defines what properties transaction must have to result in run of your action. Filters is a list and if ANY of the filters is matched, your action will run. If multiple filters are matched, you actions will still run just once. Within a filter, AND applies so transaction must match ALL fields. But that's not all. Most fields can have value or be a list of values, and if list, OR applies so transaction must match ANY value. 

Here is an example:

```
trigger:
  type: transaction
  transaction:
    status:
      - mined
      - confirmed10
    filters:
      - network: 1
        status: fail
        to: 0x8f369ae35bce72a50f1188b96d516fab425511c9
      - network:
          - 1
          - 3
        status:
          - fail
          - success
        to:
          - 0x8f369ae35bce72a50f1188b96d516fab425511c9
          - 0x2463bebe23d1b82c28d4ba8e2852d40eedde8f8b
```

String fields that you can combine in your filter are `network`, `status`, `to` and `from`.

Int fields have following spec, with all fields being optional and if multiple fields are present, AND applies:

```
gte: ? # greater or equal than
lte: ? # less or equal than
ge: ?  # greater than
le: ?  # less than
eq: ?  # equal to
```

Here is an example that filters for gas usage:

```
filters:
  - gasUsed:
      gte: 100000

filters:
  - gasUsed:  # x >= 10000 || x <= 100
      - gte: 100000
      - lte: 100
      
filters:
  - gasUsed:  # x >= 10000 && x <= 100
      gte: 100000
      lte: 100            
```

You can combine the Int fields in your filters, which are - `value`, `gasUsed`, `gasLimit`, `fee`.

More advanced transaction filters include function invocation or an event emitted on a contract \[more coming soon :tada:].

{% hint style="warning" %}
Contract must be added to your project before it can be referenced in your triggers.
{% endhint %}

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
```

{% hint style="info" %}
You can specify contract at the top of the filter and it will apply to all fields where filter is needed but it is missing.

```
filters:
  - contract:
      address: 0x8f369ae35bce72a50f1188b96d516fab425511c9
    function:
      name: stake
```
{% endhint %}

