---
description: >-
  Learn how to estimate precise gas limits for your transactions using
  simulation API.
---

# Precise Gas Estimation using Simulation API

Simulation API enables you to simulate transactions and retrieve precise gas estimation information. To enable gas estimation in your simulations, set `estimate_gas` flag to `true`.&#x20;



Example:

{% tabs %}
{% tab title="API Request" %}
```typescript
import axios from 'axios';
import * as dotenv from 'dotenv';
import { ethers } from 'ethers';
dotenv.config();

// assuming environment variables TENDERLY_USER, TENDERLY_PROJECT and TENDERLY_ACCESS_KEY are set
// https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name
// https://docs.tenderly.co/other/platform-access/how-to-generate-api-access-tokens
const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;

const mintDai = async () => {
  console.time('Simulation');
  const mint = (
    await axios.post(
      `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/simulate`,
      // the transaction
      {      
        simulation_type: 'abi', // quick, abi or full (full is default)

        network_id: '1', // network to simulate on

        from: '0xdc6bdc37b2714ee601734cf55a05625c9e512461',
        to: '0x6b175474e89094c44da98b954eedeac495271d0f',
        input:
          '0x095ea7b3000000000000000000000000f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1f1000000000000000000000000000000000000000000000000000000000000012b',
        estimate_gas: true, // flag that enables precise gas estimation
      },
      {
        headers: {
          'X-Access-Key': TENDERLY_ACCESS_KEY as string,
        },
      }
    )
  ).data;

  console.timeEnd('Simulation');
  if (mint.transaction.status == false) {
    console.log("Transaction simulation failed)
  } else {
    console.log("Gas Estimation: ", mint.transaction.gas);    
  }
};


mintDai();

```
{% endtab %}

{% tab title="API Response" %}
```json
Simulation: 136.919ms
Gas Estimation: 46098

```
{% endtab %}
{% endtabs %}
