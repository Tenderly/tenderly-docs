# Webhook

Webhook lets you trigger an action with a `POST` request.

{% hint style="success" %}
If you don't want to schedule your action and just want to run when needed with custom payload, you can set trigger type to webhook and use manual trigger.
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
curl -X POST -H "x-access-key: $TENDERLY_TOKEN" -H "Content-Type: application/json"
 # You can get this URL for your action when you open it in dashboard
 https://api.tenderly.co/api/v1/actions/$ACTION_UUID/webhook -d '{
   "dataKey": "dataValue"
}'
```

For non-authenticated webhook, it's even easier.

```bash
url -X POST -H "Content-Type: application/json"
 https://api.tenderly.co/api/v1/actions/$ACTION_UUID/webhook -d '{
   "dataKey": "dataValue"
}'
```

You can access the body from the request in runtime through WebhookEvent. In this example, `webhookEvent.payload.dataKey` will have value "dataValue"

{% hint style="warning" %}
Payload must be valid JSON and webhook endpoint will respond with 200 and `{}` if action was triggered successfully.
{% endhint %}

