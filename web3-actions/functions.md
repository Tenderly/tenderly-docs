# Functions

Functions are implemented in `actions` directory (or whatever is configured, see [configuration](https://app.gitbook.com/o/-LeLQOwIQG3HndcULLU2/s/-LeLQaB11\_TIOtLg8tIW/c/CdQUNwVtK1HwdPK4UIfp/web3-actions/configuration) page for more details. If you initialized actions project using `tenderly actions init,` you have `example.ts `(or `.js`) file which implements a function.

A function must match `ActionFn`** **[type](https://github.com/Tenderly/tenderly-actions/blob/main/packages/tenderly-actions/src/actions.ts#L4):

```typescript
import { ActionFn, BlockEvent, Context, Event } from 'tenderly-actions'

export const blockHelloWorldFn: ActionFn = async (context: Context, event: Event) => {
  let blockEvent = event as BlockEvent
  console.log(blockEvent)
}
```

{% hint style="warning" %}
You can cast event to one of `PeriodicEvent`, `WebhookEvent`, `BlockEvent` or `TransactionEvent`, but event type must match trigger type from configuration.
{% endhint %}

Or if you are using JavaScript:

```javascript
const blockHelloWorldFn = async (context, event) => {
  console.log(event)
}
module.exports = { blockHelloWorldFn }
```

If you deploy and manually trigger this action, you will see console logs when you navigate to specific execution in dashboard.

### Secrets

Secrets feature lets you securely store credentials such as API tokens that your function needs.&#x20;

Each secret is a key-value pair which is stored encrypted. To create secrets, go to dashboard and navigate to **Actions **->** Secrets**. Your secrets are available in your function through context.

```typescript
export const blockHelloWorldFn: ActionFn = async (context: Context, event: Event) => {
  const token = await context.secrets.get('API_TOKEN')
}
```

{% hint style="warning" %}
Be careful when working with secrets as logged secrets will be visible in execution logs to anyone with access to your project.
{% endhint %}

Secrets are created for each project and are available in every action in the project.

### Storage

Your actions might want to persist data across runs. You can use project's storage if you don't want to bother with external storage like your database.&#x20;

Storage is a key-value store, accessible through context. You can store up to 1000 keys, with up to 1KB in key size and 10KB in value size.

```typescript
export const blockHelloWorldFn: ActionFn = async (context: Context, event: Event) => {
    await context.storage.putNumber('LAST_BLOCK', blockEvent.blockNumber)
    await context.storage.putStr('LAST_BLOCK_HASH', blockEvent.blockHash)

    let invocationCount = await context.storage.getNumber('INVOCATIONS')
    await context.storage.putNumber('INVOCATIONS', invocationCount + 1)
}
```

You can find available getters / setters [here](https://github.com/Tenderly/tenderly-actions/blob/main/packages/tenderly-actions/src/actions.ts#L86).

Storage is shared for all actions in the project. It is recommended that you isolate using namespaces, e.g. `BLOCK_HELLO_WORLD/LAST_BLOCK` instead of just `LAST_BLOCK`.

### Development

You don't need to deploy your actions to test them. You can just run your function locally using any testing framework you like. To make this a bit easier, we are providing you with a [**testing library**](https://github.com/Tenderly/tenderly-actions/tree/main/packages/tenderly-actions-test).

Here is an example:

```typescript
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
    let result = await runtime.context.storage.get(
        'BLOCK_HELLO_WORLD/LAST_BLOCK_HASH'
    )
    expect(result).toBe('0x123456789')
});
```



Next, we are going to describe how to configure action.
