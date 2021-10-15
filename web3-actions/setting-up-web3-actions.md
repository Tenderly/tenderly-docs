# Setting Up Web3 Actions

{% hint style="warning" %}
You will need the [**Tenderly CLI**](https://github.com/Tenderly/tenderly-cli) to intialize Web3 Actions.
{% endhint %}

To get started, all you have to do is run `tenderly actions init` which will lead you through setting up a project for your Web3 Actions. 

By default, this will setup TypeScript project with `npm` but you can pass `--javascript` to use JavaScript instead.

In this example, we're going to build a block notifier, which sends us a notification whenever 10 blocks are mined on Ethereum Mainnet.

### Function

A function must match `ActionFn`** **[type](https://github.com/Tenderly/tenderly-actions/blob/main/packages/tenderly-actions/src/actions.ts#L4):

```
import { ActionFn, BlockEvent, Context, Event } from 'tenderly-actions'

export const blockNotifierFn: ActionFn = async (context: Context, event: Event) => {
  // You can cast event to one of PeriodicEvent, WebhookEvent, BlockEvent
  // or TransactionEvent, but event type must match trigger type - we'll 
  // explain triggers in a bit
	let blockEvent = event as BlockEvent

  // This is where your logic goes
  
  // You can see logs when you open an execution page in dashboard
  console.log(blockEvent.blockHash)
}
```

You can implement your function in any file/path instead your `actions` folder, but an action must reference a function in configuration. Action configuration lives in the `tenderly.yaml` file:

```
actions:
  your-project-name:
    runtime: v1  # Node 14
    sources: actions  # Folder with implementation
    specs:
      action-name:  # Must be unique for project
        description: Something something something.
        function: src/block:blockNotifierFn
```

`src/block:block:blockNotifierFn` means function `blockNotifierFn` is implemented in file `actions/src/block.ts`.

### Secrets

Secrets feature lets you securely store credentials such as API tokens that your function needs. 

Each secret is a key-value pair which is stored encrypted. To create secrets, go to dashboard and navigate to **Actions **->** Secrets**. Your secrets are available in your function through context:

```
const notificationDestinationToken = await context.secrets.get('API_TOKEN')
```

Secrets are created for each project and are available in every action in the project. [Reach out via Intercom on Tenderly Dashboard](https://dashboard.tenderly.co) if you have a need to namespace secrets and isolate between actions.

### Storage

Your actions might want to persist data across runs. You can use project's storage if you don't want to bother with external storage like your database. 

Storage is a key-value store, accessible through context. You can store up to 1000 keys, with up to 1KB in key size and 10KB in value size:

```
await context.storage.putNumber('LAST_BLOCK', blockEvent.blockNumber)
await context.storage.putStr('LAST_BLOCK_HASH', blockEvent.blockHash)

let invocationCount = await context.storage.getNumber('INVOCATIONS')
await context.storage.putNumber('INVOCATIONS', invocationCount + 1)
```

[Reach out via Intercom on Tenderly Dashboard](https://dashboard.tenderly.co) if you have a need to store more than this.

Storage is shared for all actions in the project. It is recommended that you isolate by namespacing keys, e.g. `BLOCK_NOTIFIER/LAST_BLOCK` instead of just `LAST_BLOCK`.

### Local Development

You don't need to deploy your actions to test them, you can just run your function locally using any testing framework you like. 

To make this a bit easier, we are providing you with a [**testing library here**](https://github.com/Tenderly/tenderly-actions/tree/main/packages/tenderly-actions-test).

```
test('block notifier', async () => {
		// If you use TestRuntime, you can pre-populate storage and secrets and
    // any changes to storage won't reflect in production storage
    let runtime = new TestRuntime()

    let event = new TestBlockEvent()
		event.blockHash = '0x123456789'

    runtime.context.secrets.put("API_TOKEN", "test-token")

    await runtime.execute(blockNotifierFn, event)
		
		let result = await runtime.context.storage.get(
			'BLOCK_NOTIFIER/LAST_BLOCK_HASH'
		)
    expect(result).toBe('0x123456789')
});
```

