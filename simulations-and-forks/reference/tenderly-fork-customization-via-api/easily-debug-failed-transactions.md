---
description: >-
  Learn how to persist simulation data on Tenderly and use it to examine failed
  or successfully executed transaction simulations.
---

# Easily Debug Failed Transactions

By default, transactions executed via API don’t persist on Tenderly and aren't visible in the Dashboard. When executing simulations, you probably want to examine them in greater detail.

When running a transaction simulation, you can provide the `save_if_fails` flag. So, if a failure takes place, the simulation data will be persisted in the Tenderly Dashboard.

If you need to save the simulation of a successfully executed transaction, you can set the `save` flag (`false` by default).

Additionally, the response you receive contains the simulation ID (`simulation.id`), so you can generate a link directly to Tenderly Debugger. This helps you speed up the time needed to understand and fix a bug or any other issue that is present in the smart contract.

```tsx
...
const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;

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
