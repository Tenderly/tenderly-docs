---
description: >-
  Learn how to estimate precise gas limits for your transactions using
  simulation API.
---

# Precise Gas Estimation using Simulation API

The Simulation API provides developers with the ability to simulate transactions and obtain accurate gas estimation details. By utilizing this API, you can replicate the execution of transactions without actually executing them on the blockchain network. This simulation process allows you to retrieve precise information about the gas estimation that needs to be passed in a transaction in order for execution to be successful.

To activate gas estimation during your simulations, you need to specify the "estimate\_gas" flag and set it to true. By enabling this flag, you inform the simulation process to calculate and provide an estimation of the gas limit required for the transaction. Gas limit refers to the maximum amount of computational work that a transaction can perform within the blockchain network.

Once the simulation is conducted and the status of the process is reported as successful, you can access the detailed gas limit estimation within the transaction structure. Specifically, this information will be available in the `gas` field of the `transaction` structure. By examining this field, developers can obtain the precise gas limit estimation for the simulated transaction, enabling them to make informed decisions and optimizations regarding gas usage in their blockchain applications.



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
