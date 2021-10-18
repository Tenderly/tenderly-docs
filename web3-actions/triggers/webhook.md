# Webhook

Webhook lets you trigger an action with a `POST` request. You can decide if the request should be authenticated or not. If it should be authenticated you must make a request with a valid Tenderly token that can access this action's project.

```
trigger:
  type: webhook
  webhook:
    authenticated: true
```

To trigger an action, get the UUID for your action from your dashboard, and make the following `POST` request:

```
curl -X POST -H "x-access-key: $TENDERLY_TOKEN" -H "Content-Type: application/json"
 https://api.tenderly.co/api/v1/actions/$ACTION_ID/webhook -d '{
   "myData": "myValue"
}'
```

You can access the body from the request through the event `webhookEvent.payload.myData`.
