# Triggers

A **trigger** determines on which event or by which schedule your function will be executed.&#x20;

Trigger also defines the event type for your action, so `block` trigger will result in your function getting `BlockEvent`. [**Take a look at our API**](https://github.com/Tenderly/tenderly-actions/blob/main/packages/tenderly-actions/src/actions.ts) to better understand what each event type has (or log event to console, use manual trigger and check out the output).

Check our docs for specific trigger type that you are

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

Action trigger is configured in `tenderly.yaml`, if you haven't already, see [configuration](https://app.gitbook.com/o/-LeLQOwIQG3HndcULLU2/s/-LeLQaB11\_TIOtLg8tIW/c/CdQUNwVtK1HwdPK4UIfp/web3-actions/configuration) page.&#x20;
