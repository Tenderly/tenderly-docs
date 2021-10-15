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

{% content-ref url="periodic.md" %}
[periodic.md](periodic.md)
{% endcontent-ref %}

{% content-ref url="webhook.md" %}
[webhook.md](webhook.md)
{% endcontent-ref %}

{% content-ref url="block.md" %}
[block.md](block.md)
{% endcontent-ref %}

{% content-ref url="transaction.md" %}
[transaction.md](transaction.md)
{% endcontent-ref %}
