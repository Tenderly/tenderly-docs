# Easily Debug Failed Transactions

By default, transactions executed via API don’t persist in Tenderly and are not visible in the dashboard. When you execute Simulations you probably need to examine why they failed.

When running a transaction Simulation you can provide the `save_if_fails` flag. In case of a failure, it will be persisted in the Tenderly Dashboard.

If you need to save the Simulation of a successfully executed transaction, you can set the `save` flag (`false` by default).

Additionally, the response you receive will contain simulation ID (`simulation.id`), so you can generate a link directly to the Tenderly Debugger. This would help you speed up the time needed to understand and fix the bug or any other issue that is present in the smart contract.

```tsx
...

const body = {
  "network_id": "1",
  "from": senderAddr,
  "to": contract.address,
  "input": unsignedTx.data,
  "gas": 21204,
  "gas_price": "0",
  "value": 0,
  "save_if_fails": true
}

const opts = {
  headers: {
    'content-type': 'application/JSON',
    'X-Access-Key': TENDERLY_ACCESS_KEY,
  }
}
const resp = await axios.post(apiURL, body, opts);

if (simulation.status == "failed") {
  const link = `https://dashboard.tenderly.co/project/${TENDERLY_PROJECT_SLUG}/simulator/${resp.data.simulation.id}`
  // trigger sentry, log error, make the test fail if in test
}
```
