---
description: >-
  Learn more about using Simulation API for highly customized transaction
  simulations and extracting decoded simulation data.
---

# Advanced Simulation API

In this code sample, we'll be using Simulation API to extract and show the following information:

* State changes
* Events emitted during the simulated transaction execution
* Output values of the called smart contract function
* Balance changes
* A transaction simulated in a past block, at a particular block index

We'll simulate the execution of an existing successful transaction sent to UniswapV2Router02 on the Ethereum Mainnet to retrieve additional information.&#x20;

Here's the transaction calling `swapExactTokensForTokens()` and exchanging 3,118.71 XCAD to USDT.

```json
{
  "from": "0x1cf5cd427d0a968379bd6b5befce28d8e157ae38",
  "input": "0x8803dbee00000000000000000000000000000000000000000000009df85158cbf910000000000000000000000000000000000000000000000000000000000000c65a511800000000000000000000000000000000000000000000000000000000000000a00000000000000000000000001cf5cd427d0a968379bd6b5befce28d8e157ae380000000000000000000000000000000000000000000000000000000063d9ac890000000000000000000000000000000000000000000000000000000000000002000000000000000000000000dac17f958d2ee523a2206206994597c13d831ec70000000000000000000000007659ce147d0e714454073a5dd7003544234b6aa0",
  "to": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
  "gas": 138864,
  "gas_price": "32909736476",
  "value": "0",
  "access_list": []
}
```

The following code customizes the simulation context by:

* simulating the transaction on the block 16533181.
* simulating this transaction as the first transaction within that block.
* performing a **full** simulation.

{% tabs %}
{% tab title="Request" %}
```typescript
import axios from 'axios';
import * as dotenv from 'dotenv';
dotenv.config();

const simulateUniswap = async () => {
  // assuming environment variables TENDERLY_USER, TENDERLY_PROJECT and TENDERLY_ACCESS_KEY are set
  // https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name
  // https://docs.tenderly.co/other/platform-access/how-to-generate-api-access-tokens
  const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;

  const resp = await axios.post(
    `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/simulate`,
    // the transaction
    {
      // Simulation configuration
      save: true, // if true simulation is saved and shows up in the dashboard
      save_if_fails: true, // if true, reverting simulations show up in the dashboard
      simulation_type: 'full', // full or quick (full is default)

      // network to simulate on
      network_id: '1',
      // simulate transaction at this (historical) block number
      block_number: 16527769,
      // simulate transaction at this index within the (historical) block
      transaction_index: 42,

      /* Standard EVM Transaction object */
      from: '0x1cf5cd427d0a968379bd6b5befce28d8e157ae38',
      input:
        '0x8803dbee00000000000000000000000000000000000000000000009df85158cbf910000000000000000000000000000000000000000000000000000000000000c65a511800000000000000000000000000000000000000000000000000000000000000a00000000000000000000000001cf5cd427d0a968379bd6b5befce28d8e157ae380000000000000000000000000000000000000000000000000000000063d9ac890000000000000000000000000000000000000000000000000000000000000002000000000000000000000000dac17f958d2ee523a2206206994597c13d831ec70000000000000000000000006b175474e89094c44da98b954eedeac495271d0f',
      to: '0x7a250d5630b4cf539739df2c5dacb4c659f2488d',
      gas: 138864,
      gas_price: '32909736476',
      value: '0',
      access_list: [],
      generate_access_list: true,
    },
    {
      headers: {
        'X-Access-Key': TENDERLY_ACCESS_KEY as string,
      },
    }
  );

  // access the transaction object
  const transcation = resp.data.transaction;

  // access the transaction call trace
  const callTrace = transcation.transaction_info.call_trace;

  // access transaction's logs
  const logs = resp.data.transaction.transaction_info.logs;

  console.log(
    `Simulated transaction info: hash: ${transcation.hash} block number: ${transcation.block_number}`
  );

  // display balance changes
  console.log(
    'Balance changes',
    '\n  ' +
      callTrace.balance_diff
        .map(
          (balance: any) =>
            `${balance.address}: ${balance.original} -> ${balance.dirty} ${
              balance.is_miner ? '(Miner)' : ''
            }`
        )
        .join('\n  ')
  );

  // display output values
  console.log(
    'Output values' +
      '\n  ' +
      callTrace.decoded_output
        .map(
          (output: any) =>
            `${output.soltype.name} ${output.soltype.type} = ${JSON.stringify(
              output.value
            )}`
        )
        .join('\n  ')
  );

  // display events
  console.log(
    'Events' +
      '\n  ' +
      logs
        .map(
          (log: any) =>
            `${log.name} (${log.inputs
              .map(
                (input: any) =>
                  `${input.soltype.name} ${input.soltype.type} = ${input.value}`
              )
              .join(', ')})`
        )
        .join('\n  ')
  );

  const stateDiff = resp.data.transaction.transaction_info.state_diff;

  // display state changes for all affected contracts
  console.log(
    'State changes' +
      '\n  ' +
      stateDiff
        .map(
          (diff: any) =>
            `${diff.address}
  ${diff.soltype.name}: ${diff.soltype.type}
    ${JSON.stringify(diff.original)} -> ${JSON.stringify(diff.dirty)}
  `
        )
        .join('\n  ')
  );
};

simulateUniswap();
```
{% endtab %}

{% tab title="Result" %}
```json
Simulated transaction info: hash: 0xcec4137280bdb736a3e36a2d8057c1c6abd710f8950383d545c6e83e79de83d4 block number: 16527769
Balance changes 
  0x1cf5cd427d0a968379BD6b5BefcE28d8e157AE38: 178649986537506409 -> 174451493996844233 
  0xC0E1b256DE232262134c22f73b21F756072Bfb73: 4913764247259774380 -> 4913891833847051468 (Miner)
Output values
  amounts uint256[] = ["2925968626","2914031999999999475712"]
Events
  Transfer (from address = 0x1cf5cd427d0a968379bd6b5befce28d8e157ae38, to address = 0xb20bd5d04be54f870d5c0d3ca85d82b34b836405, value uint256 = 2925968626)
  Transfer (from address = 0xb20bd5d04be54f870d5c0d3ca85d82b34b836405, to address = 0x1cf5cd427d0a968379bd6b5befce28d8e157ae38, value uint256 = 2914031999999999475712)
  Sync (reserve0 uint112 = 3406489853911049758294153, reserve1 uint112 = 3413108350557)
  Swap (sender address = 0x7a250d5630b4cf539739df2c5dacb4c659f2488d, amount0In uint256 = 0, amount1In uint256 = 2925968626, amount0Out uint256 = 2914031999999999475712, amount1Out uint256 = 0, to address = 0x1cf5cd427d0a968379bd6b5befce28d8e157ae38)
State changes
  0x6b175474e89094c44da98b954eedeac495271d0f
  balanceOf: mapping (address => uint256)
    {"0x1cf5cd427d0a968379bd6b5befce28d8e157ae38":"0","0xb20bd5d04be54f870d5c0d3ca85d82b34b836405":"3409403885911049757769865"} -> {"0x1cf5cd427d0a968379bd6b5befce28d8e157ae38":"2914031999999999475712","0xb20bd5d04be54f870d5c0d3ca85d82b34b836405":"3406489853911049758294153"}
  
  0xb20bd5d04be54f870d5c0d3ca85d82b34b836405
  reserve0: uint112
    "3409403885911049757769865" -> "3406489853911049758294153"
  
  0xb20bd5d04be54f870d5c0d3ca85d82b34b836405
  reserve1: uint112
    "3410182381931" -> "3413108350557"
  
  0xb20bd5d04be54f870d5c0d3ca85d82b34b836405
  blockTimestampLast: uint32
    1675177403 -> 1675179707
  
  0xb20bd5d04be54f870d5c0d3ca85d82b34b836405
  price0CumulativeLast: uint256
    "441576621729456416380537755631" -> "441588587513036279679286478575"
  
  0xb20bd5d04be54f870d5c0d3ca85d82b34b836405
  price1CumulativeLast: uint256
    "439308598518790202534497963032180663370642780076827973" -> "439320558839758057121212644076286195263865870112652613"
  
  0xdac17f958d2ee523a2206206994597c13d831ec7
  balances: mapping (address => uint256)
    {"0x1cf5cd427d0a968379bd6b5befce28d8e157ae38":"22963773121","0xb20bd5d04be54f870d5c0d3ca85d82b34b836405":"3410182381931"} -> {"0x1cf5cd427d0a968379bd6b5befce28d8e157ae38":"20037804495","0xb20bd5d04be54f870d5c0d3ca85d82b34b836405":"3413108350557"}
```
{% endtab %}
{% endtabs %}
