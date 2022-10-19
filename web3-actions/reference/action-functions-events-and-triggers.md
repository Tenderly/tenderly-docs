---
description: >-
  Explore details behind the core elements of Web3 Actions, learn how to specify
  trigger configurations for supported events, and link triggers to action
  functions in tenderly.yaml.
---

# Action Functions, Events, and Triggers

This guide presents the three core concepts of Web3 Actions: **triggers, events, and functions**. You’ll learn how they work and how to use them to build your own Web3 Actions.

The three core components that make up a Web3 Action are:

* **Functions:** Custom JavaScript or TypeScript code you want to execute when an external event occurs. This is the core of your automation.
* **Triggers:** Pre-defined external events that your Web3 Action is configured to listen for. When the event occurs, the trigger instructs Tenderly to execute your custom code (function).
* **Events (Trigger Types):** Pre-defined external events that you can listen for by setting a trigger. When the event occurs, the trigger will call your custom code (functions).

### Action functions

Web3 Action functions refer to the custom code written as standard JavaScript or TypeScript functions, but they must adhere to some rules.

* Functions must be asynchronous, returning `Promise<void>`
* Functions accept two parameters: `context` and `event`
* Functions must be a named export from the file
* Functions can be placed in any file under the _actions root_ directory

Learn about the [Web3 Actions project and file structure](project-structure.md).

When a Web3 Action function is deployed, the Tenderly runtime will pass the following arguments during invocation:

* The `context` parameter that holds access to [Storage and Secrets](context-storage-and-secrets.md).
* The `event` parameter that is an object with information answering the question _“what just happened?_”. This parameter contains data specific to the trigger type the Web3 Action function is listening for. The section [Specifying triggers for external events](action-functions-events-and-triggers.md#specifying-triggers-for-external-events) goes into detail about external events.

{% hint style="info" %}
The execution of Web3 Action functions is limited to 20 seconds. If your function takes longer than 20 seconds to execute, it will be terminated.
{% endhint %}

Here’s an example of a Web3 Action function written in TypeScript. The `event` parameter can be any one of the supported trigger types (events).

```typescript
// File: actions/myCoolTsFile.ts
import {
  ActionFn, Context,
  Event, BlockEvent, PeriodicEvent, TransactionEvent, WebhookEvent
} from "@tenderly/actions";

// importing ethers available in Tenderly Runtime
import { ethers } from "ethers";

export const awesomeActionFunction: ActionFn = async (context: Context, event: Event) => {
  // cast the event parameter to an appropriate type, based on the Trigger
  // this function subscribed to.
  // Of course, only one of these casts makes sense
  const blockEvent = event as BlockEvent;
  const periodicEvent = event as PeriodicEvent;
  const transactionEvent = event as TransactionEvent;
  const webhookEvent =  event as WebhookEvent;
	...
}
```

#### Available libraries for dashboard-based actions

The Tenderly runtime comes pre-bundled with several javascript libraries that you can import when creating Web3 Actions via the Tenderly Dashboard. Available libraries include:

* [Ethers.js](https://docs.ethers.io/v5/)
* [Bignumber.js](https://mikemcl.github.io/bignumber.js/)
* [Axios](https://axios-http.com/docs/intro)
* [Luxon](https://moment.github.io/luxon/#/?id=luxon)

To import any of these libraries, use the `require()` function as you would with a standard npm-based project (without ES6).

Example import for Axios looks like this:

```jsx
const axios = require("axios");
```

#### Using npm libraries for CLI-based Web3 Actions

The project created by Tenderly CLI is in fact an npm module. You can install any npm package from your _actions root_ folder.

### External events and trigger types

When an external event happens, it _triggers the execution of your custom code_ (functions). You can choose between four external events to listen for:

* **Block event**: A block is mined on a selected network.
* **Periodic event:** This trigger happens when certain time intervals pass or based on CRON expressions.
* **Webhook event:** An HTTP request is posted to the webhook URL (the Web3 Action exposes a webhook)
* **Transaction event:** A transaction matching given filter criteria is executed on a selected network.

When defining a Web3 Action, you'll be effectively defining triggers that react to external events of interest for your project. In the context of trigger specification, we'll be using the term **trigger type**.

{% hint style="success" %}
You should write separate functions for each trigger type. Using the same function for different trigger types is not recommended.
{% endhint %}

### Subscribing Web3 Action functions to events

In addition to defining your action function in JavaScript, you also need to provide the trigger configuration, which tells Tenderly **what triggers it — the external event your function subscribes to.**

When creating Web3 Actions via the Tenderly Dashboard, the creation flow in the UI will handle this part for you. Read the [Dashboard Quickstart](../tutorials-and-quickstarts/deploy-web3-actions-via-dashboard.md) guide.

When working with code-based Web3 Actions, functions and their triggers must be defined in the `tenderly.yaml` file, which is generated by Tenderly CLI. Read the [CLI Quickstart](../tutorials-and-quickstarts/deploy-web3-action-via-cli.md) guide.

**Example**

In the example below, we’re declaring a Web3 Action called **bestActionEver** and referencing the function **awesomeActionFunction** that is exported from the **actions/myCoolTsFile.ts** file. This is the function that Tenderly will call when the Web3 Action gets triggered.

```yaml
account_id: ""
actions:
  our-cool-org/our-cool-project:
    runtime: v1
    sources: actions
    specs:
      bestActionEver:
        description: Does the best thing ever
        function: myCoolTsFile:awesomeActionFunction
        trigger:           # trigger declaration start
          type: ...        # type
          ...              # configuration map (external event specific)
```

### Specifying triggers for external events

In this section, we’ll examine the `trigger` declaration. For more information on writing tenderly.yaml file, reference [this guide](project-structure.md#the-tenderly.yaml-file-structure).

The trigger type and corresponding configurations are defined in the **tenderly.yaml** file. You first must define the `trigger` object, which has two mandatory properties:

* The `type` property, that specifies the trigger type, which can be: `periodic | webhook | block | transaction`
* An object with a configuration specific to the selected trigger type

Below is a detailed explanation of the trigger-specific configurations for each trigger type.

### Periodic event

A periodic event is used when you want your Web3 Action to be triggered at specific time intervals. It carries **time**: the time of invocation.

```typescript
type PeriodicEvent = {
  time: Date;
};
```

The trigger declaration has the `periodic` type. It can be interval- or cron-based:

```yaml
trigger:
  type: periodic
  periodic:
    interval: 5m
```

The `interval` property can take any of the following values: `5m | 10m | 15m | 30m | 1h | 3h | 6h | 12h | 1d`

Use the CRON-based periodic trigger if you need more granular control over when your Web3 Action gets executed:

```yaml
trigger:
  type: periodic
  periodic:
    cron: "5 */1 * * *"
```

The `cron` property can be any valid [CRON string](https://crontab.guru/).

### Webhook event

Webhook-based Web3 Actions expose a custom webhook URL, making it possible to trigger them from external systems using a simple HTTP POST request.

The corresponding trigger type holds two properties: the **time** of invocation and any **payload** (a JSON object). Tenderly doesn't perform any validation or inspections on your payload.

```typescript
type WebhookEvent = {
  time: Date;
  payload: any;
};
```

A trigger configuration example:

```yaml
trigger:
  type: webhook
  webhook:
    authenticated: true
```

If `authenticated` is set to **true**, you must include the Tenderly Access Token with your request to be able to run the Web3 Action as the value of `x-access-key`. You can find the cURL of the exposed webhook in the Web3 Action overview in the Tenderly Dashboard.

```bash
curl -X POST \
-H "x-access-key: $ACCESS_TOKEN" \
-H "Content-Type: application/json" \
https://api.tenderly.co/api/v1/actions/7acc7db2-00d6-4872-b2d2-d9430bd8fe7b/webhook \
-d '{"foo": "bar"}'
```

### Block event

The block event is used when you want to listen for the mining of blocks on one or several networks. You can make your Web3 Action "block-periodic" by specifying the number of mined blocks between two consecutive invocations.

```typescript
type BlockEvent = {
  blockHash: string;
  blockNumber: number;
  network: string;
};
```

When declaring the block trigger, you can specify the following properties:

* `network`: a single value or a list of [network IDs](https://docs.tenderly.co/web3-actions/intro-to-web3-actions/networks) you’re interested in
* `blocks`: the number of mined blocks between two consecutive executions of the Web3 Action. For example, execute the Web3 Action on every 100th block mined.

```yaml
trigger:
  type: block
  block:
    network:
      - 1
      - 42
    blocks: 100
```

### Transaction event

The transaction trigger type allows you to listen for specific transactions as they get executed on-chain.

{% hint style="info" %}
To listen for transactions from a smart contract, the smart contract must be verified and added to your project in the Tenderly Dashboard. The CLI will throw a warning if this is not the case.
{% endhint %}

You can specify different conditions in the form of **filters** to zero in on transactions of interest. Your custom code will be invoked with that exact transaction payload passed through the `event` parameter.

```typescript
type TransactionEvent = {
  blockHash: string;
  blockNumber: number;
  from: string;
  hash: string;
  network: string;
  to?: string;
  logs: Array<{
    address: string;
    data: string;
    topics: string[];
  }>;
  input: string;
  value: string;
  nonce: string;
  gas: string;
  gasUsed: string;
  cumulativeGasUsed: string;
  gasPrice: string;
  gasTipCap: string;
  gasFeeCap: string;
  transactionHash: string;
};
```

When listening for transaction events, you can also specify the following settings:

* **Transaction mining status**: `mined` (the transaction has been mined) or `confirmed10` (10 blocks are confirmed since the block that contains the transaction)
* **Filters:** A list of conditions involving transaction payload using the `filters` list. Only transactions that match filters will trigger the execution of your code.

#### Filtering transactions

The `filters` list allows you to define triggering criteria using transaction properties to match specific transactions.

The `filters` list **acts as a logical disjunction of individual filters** (elements of the list). This means that only those transactions that match any individual filter from the list will trigger the execution of the Web3 Action.

A single filter (element of the list) is an object comprised of several logical conditions. If all conditions are met, the criteria of the filter as a whole are met. In other words, **the filter object acts as a logical conjunction of individual conditions**.

Below is a list of all available filters you can combine to build criteria for transactions that will trigger the execution of your Web3 Action.

| Filter                                                        | Description                                                                                                                                                                                                                                                                   |
| ------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>*mandatory <br>**at least one of these must be present</p> |                                                                                                                                                                                                                                                                               |
| network\*                                                     | The network ID from which the transaction originated                                                                                                                                                                                                                          |
| status                                                        | The transaction status: fail or success                                                                                                                                                                                                                                       |
| from\*\*                                                      | The address of the transaction originator                                                                                                                                                                                                                                     |
| to\*\*                                                        | The address of the transaction recipient                                                                                                                                                                                                                                      |
| eventEmitted                                                  | An event of a specific type, emitted by a particular contract                                                                                                                                                                                                                 |
| logEmitted\*\*                                                | Logs emitted by a particular contract, by matching the prefix of the raw log entry                                                                                                                                                                                            |
| function\*\*                                                  | Direct call to the given function. Not applicable to internal calls between the contracts                                                                                                                                                                                     |
| value                                                         | The value that is transferred within the transaction in wei                                                                                                                                                                                                                   |
| gasUsed                                                       | The amount of gas used by the transaction in wei                                                                                                                                                                                                                              |
| gasLimit                                                      | The gas limit set for the transaction in wei                                                                                                                                                                                                                                  |
| effectiveGasPrice                                             | <p>Price per gas for transaction’s execution, used to calculate the effective price of transaction’s execution, as per EIP-1599:<br><code>block.base_fee_per_gas + min(transaction.max_priority_fee_per_gas, transaction.max_fee_per_gas - block.base_fee_per_gas)</code></p> |

{% hint style="warning" %}
A trigger must contain `network` and at least one of the following filters:\
`from`, `to`, `function`, `eventEmitted` or `logEmitted`
{% endhint %}

An **example** of a transaction coming on network 1 sent to `0x236..fd62`.

```yaml
failedTransactionToMyContract:
  description: When sent to my contract fails
  function: observingTransactions:failedAttempts
  trigger:
    type: transaction
    transaction:
      status:
        - mined
      filters:
        # Transaction must be from the network with network ID 1 (mainnet)
        - network: 1
          # Transaction must have failed
          status: fail
          # Transaction must have been sent to this address
          to: 0x2364259ACD20Bd2A8dEfDc628f4099302449fd62
          # transaction must have involved this contract
          contract:
            address: 0xad881d3d06c7f168715b84b54f9d3e1ff27b80d6
        - network: 3
          # Transaction must have failed
          status: success
          # Transaction must have been sent to this address
          to: 0x2364259ACD20Bd2A8dEfDc628f4099302449fd62
```

In this case, we're interested only in transactions that are mined, such that they touched the contract deployed at `0xad88...80d6` and resulted in a runtime failure, sent to address `0x2364...fd62` on network 1 or transactions that resulted in successful execution, sent to the same address on network 3.

This would equate to the following JavaScript code:

```jsx
tx.status == "mined" &&
  // filters list
  // filter 1
  ((tx.network == 1 &&
    tx.status == "fail" &&
    tx.to == "0x2364259ACD20Bd2A8dEfDc628f4099302449fd62" &&
    contract.address == "0xad881d3d06c7f168715b84b54f9d3e1ff27b80d6") ||
    // filter 2
    (tx.network == 3 &&
      tx.status == "success" &&
      tx.to == "0x2364259ACD20Bd2A8dEfDc628f4099302449fd62"));
```

Since we didn't filter by any particular sender, all transactions coming to the mentioned recipient will result in the Web3 Action being triggered.

#### Filtering transactions by transaction fields

Among the common transaction fields, you can filter by the following properties having specific values.

* `from: 0xDB6...BbE1` - filtering on a specific sender. Optional.
* `to: 0x2364...fd62` - filtering on a specific receiver. Optional.
* `status: fail|success` - filtering on transaction status. Optional.
* `network: 3` - filtering only transactions coming from network 3. Mandatory.
* `contract.address` - filtering only transactions involving the contract with this specific address. Optional.

You can also query numerics related to exchanged value and gas, using relational operators. All of the following are in **wei**:

* `value`
* `gasUsed`,
* `gasLimit`,
* `effectiveGasPrice`

You can use any of the common comparison operators: `eq`, `gte`, `gt`, `lt`, `lte`.

Below is an example of a filter demonstrating filters using scalar values in the transaction payload.

```yaml
filters:
    - network: 1
      value:
       eq: 120
      gas:
        gt: 100
        lt: 150
      gasLimit:
        lt: 200
      fee:
        gte: 140
      gasPrice:
        lte: 120
      nonce:
        gt: 20
```

This example filter will take only transactions where the following expression holds:

```js
tx.value == 120 &&
  tx.gas > 100 &&
  tx.gas < 150 &&
  tx.gasLimit < 200 &&
  fee >= 140 &&
  gasPrice <= 120 &&
  nonce > 20;
```

#### Filtering transactions using emitted EVM Events

Configuring Web3 Actions to listen for EVM events emitted by a transaction execution allows you to respond to significant changes logged by these events. You can achieve this by using the `eventEmitted` operator, which supports the following nested properties:

* `contract` (mandatory): To specify the origin of the event. The `contract.address` must be used to specify the address of the contract that emitted the event.
* `name` (mandatory): To specify the name of the event.

{% hint style="info" %}
To use the `eventEmitted` filter, the contract must be verified and added to the project in the Tenderly Dashboard.
{% endhint %}

Below is an example of a Web3 Action that will be invoked when either `TxSubmission` or `TxConfirmation` event is emitted when the smart contract is executed at the address `0x418d..9d45` on network 3.

```yaml
txSubmittedOrConfirmed:
  description: When any of TxSubmission and TxConfirmation is emitted
  function: myCoolJsFile:myC
  trigger:
    type: transaction
    transaction:
      filters:
        - network: 3
          eventEmitted:
            contract:
              address: 0x418ebb95eaa40c119408143056cad984c6129d45
            name: TxSubmission
        - network: 3
          eventEmitted:
            contract:
              address: 0x418ebb95eaa40c119408143056cad984c6129d45
            name: TxConfirmation
```

#### Filtering transactions by emitted logs

Another way to listen for EVM events is to query them by the log topic.

The `logEmitted` filter must include:

* `contract.address`: The source of the logs
* `startsWith`: A list of raw prefixes of the log topics. If an event log exists such that it’s prefixed by one of the elements in this list, the Web3 Action function will be triggered.

{% hint style="info" %}
Using `logEmitted` enables you to use the event topic prefix in its raw form to filter for events. This is useful if you’re setting up a Web3 Action on an unverified contract.
{% endhint %}

Below is an example of a Web3 Action that will be invoked when a transaction contains log entries starting with the given prefixes.

```yaml
txEmittedSomeLogs:
  description: When particular logs are emitted
  function: observingTransactions:someLogsEmittedAction
  trigger:
    type: transaction
    transaction:
      filters:
        - network: 3
          # Transaction must come from the network with network ID 5
          logEmitted:
            # Transaction must have emitted a log entry
            contract:
              address: 0x418ebb95eaa40c119408143056cad984c6129d45
              # coming from the contract at this address
            startsWith:
              # and topics of the log entry must start with either one of these
            - 0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef
            - 0x0000000000000000000000000000000000000000000000000000000000000000
```

#### Filtering transactions involving a specific contract

To filter for transactions that call a specific contract during their execution (i.e. internal calls), you can use the optional `contract.address` filter.

In the example below, both filters will retain transactions on the network 3 sent to `0x2364...fd62.` The second filter is more restrictive: only those involving contract `0xad88...80d6` will trigger the Web3 Action functions.

```yaml
failedTransactionToMyContract:
  description: When sent to my contract fails
  function: observingTransactions:failedAttempts
  trigger:
    type: transaction
    transaction:
      status:
        - mined
      filters:
        - network: 5
          # Transaction must come from the network with network ID 5
          status: success
          # Transaction must have succeeded
          to: 0x2364259ACD20Bd2A8dEfDc628f4099302449fd62
          # Transaction must have been sent to this address
        - network: 5
          # Transaction must come from the network with network ID 5
          status: success
          # Transaction must have succeeded
          to: 0x2364259ACD20Bd2A8dEfDc628f4099302449fd62
          # transaction must have involved the following contract
          contract:
            address: 0xad881d3d06c7f168715b84b54f9d3e1ff27b80d6
```

#### Filtering transactions with a direct call to a function

To filter for transactions that directly call a specific function, you can use the optional `function` filter. It requires the address of the contract `contract.address` and the `name` of the function.

This applies only to direct calls of the specified function, coming from an EOA. Internal calls aren’t taken into account.

Below is an example of a Web3 Action trigger responding to a direct call to the `verySpecialFunction` of the contract deployed at `0xad88...80d6`.

```yaml
failedTransactionToMyContract:
  description: When sent to my contract fails
  function: observingTransactions:failedAttempts
  trigger:
    type: transaction
    transaction:
      status:
        - mined
      filters:
        # Transaction must be from the network with network ID 1 (mainnet)
        - network: 1
          # Transaction must have failed
          status: fail
          function:
            # the function verySpecialFunction must have been called directly
            name: verySpecialFunction
            contract:
              address: 0xad881d3d06c7f168715b84b54f9d3e1ff27b80d6tyty
```
