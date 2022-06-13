# Functions

Functions are implemented in the `actions` directory (or whatever is configured, see **** [**configuration**](configuration.md) **** page for more details. If you initialized actions project using `tenderly actions init,` you have `example.ts` (or `.js`) file which implements a function.

A function must match `ActionFn` **** [**type**](https://github.com/Tenderly/tenderly-actions/blob/main/packages/actions/src/actions.ts):

```typescript
import { ActionFn, BlockEvent, Context, Event } from '@tenderly/actions'

export const blockHelloWorldFn: ActionFn = async (context: Context, event: Event) => {
  let blockEvent = event as BlockEvent
  console.log(blockEvent)
}
```

Or for other types of trigger:

```typescript
let transactionEvent = event as TransactionEvent
let periodicEvent = event as PeriodicEvent
let webhookEvent = event as WebhookEvent
```

{% hint style="warning" %}
Event type must match trigger type for a given action from the configuration.
{% endhint %}

Or if you are using JavaScript:

```javascript
const blockHelloWorldFn = async (context, event) => {
  console.log(event)
}
module.exports = { blockHelloWorldFn }
```

If you deploy and manually trigger this action, you will see console logs when you navigate to specific execution in the dashboard.

### Secrets

Secrets feature lets you securely store credentials such as API tokens that your function needs.&#x20;

Each secret is a key-value pair which is stored encrypted. To create secrets, go to dashboard and navigate to **Actions** -> **Secrets**. Your secrets are available in your function through context.

```typescript
export const blockHelloWorldFn: ActionFn = async (context: Context, event: Event) => {
  const token = await context.secrets.get('API_TOKEN')
}
```

{% hint style="danger" %}
Be careful when working with secrets as logged secrets will be visible in execution logs to anyone with access to your project.
{% endhint %}

Secrets are created for each project and are available in every action in the project.

### Storage

Your actions might want to persist data across runs. You can use the project's storage if you don't want to bother with external storage like your database.&#x20;

Storage is a key-value store, accessible through context. You can store up to 1000 keys, with up to 1KB in key size and 10KB in value size.

```typescript
export const blockHelloWorldFn: ActionFn = async (context: Context, event: Event) => {
    await context.storage.putNumber('HELLO_WORLD/BLOCK_NUMBER', event.blockNumber)
    await context.storage.putStr('HELLO_WORLD/BLOCK_HASH', event.blockHash)

    let invocationCount = await context.storage.getNumber('HELLO_WORLD/INVOCATIONS')
    await context.storage.putNumber('HELLO_WORLD/INVOCATIONS', invocationCount + 1)
}
```

You can find available getters/setters in the Storage interface [**here**](https://github.com/Tenderly/tenderly-actions/blob/main/packages/actions/src/actions.ts).

{% hint style="success" %}
If you read a key that does not exist from storage, you will get default value based on a getter you used:&#x20;

* `getNumber` returns number 0
* `getBigInt` returns BigInt(0)
* `getStr` returns an empty string
* `getJson` returns an empty object
{% endhint %}

Storage is shared for all actions in the project. It is recommended that you isolate using namespaces, e.g.`HELLO_WORLD/BLOCK_NUMBER` instead of just `BLOCK_NUMBER`.

When using a manual trigger, you must choose the storage type. You can choose between creating a new empty storage (`EMPTY`), use project's storage (`WRITE`) or create new storage from the project's storage (`COPY_ON_WRITE`). For example, if the project's storage has `INVOCATION = 1` and your action reads and increments this key:

* if you use `EMPTY` the result will be `1` - incremented from default 0
* if you use `WRITE` the result will be `2` and it will be visible in the project's storage
* if you use `COPY_ON_WRITE` the result will be `2` but it won't be visible in the project's storage

{% hint style="danger" %}
Be careful when using `WRITE` storage type. Changes will be persisted in the project's storage and there is currently no way to roll back changes made by specific execution of an action.
{% endhint %}

### Development and Testing

If your action logic is more complex (and it's maybe not working as expected) you might want to use a debugger. You can avoid deploying your action to test it if you setup local development. To make this a bit easier, we are providing you with a [**testing library**](https://github.com/Tenderly/tenderly-actions/tree/main/packages/actions-test). Here is an example how to use this library to execute an action in unit tests:

```typescript
import { TestRuntime, TestBlockEvent } from "@tenderly/actions-test";

test('block hello world', async () => {
    // If you use TestRuntime, any changes to storage won't reflect
    // in production storage.
    let runtime = new TestRuntime()
    
    // Test* events are available for other types.
    let event = new TestBlockEvent()
    event.blockHash = '0x123456789'

    // If you use TestRuntime, you can pre-populate secrets.
    // In real runtime, you can add secrets through dashboard only.
    runtime.context.secrets.put("API_TOKEN", "test-token")

    // Run function.
    await runtime.execute(blockHelloWorldFn, event)

    // Verify storage was modified as expected.
    // This checks in-memory test storage and not a real production storage!			
    let result = await runtime.context.storage.getStr(
        'BLOCK_HELLO_WORLD/LAST_BLOCK_HASH'
    )
    expect(result).toBe('0x123456789')
});
```



Next, we are going to describe how to configure an action.
