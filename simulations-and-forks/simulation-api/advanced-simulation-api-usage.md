---
description: Learn how to use simulation API to extract transaction information.
---

# Advanced Simulation API Usage

In this code sample, we use Simulation API to:

* Simulate a transaction in a past block, at a particular block index.
* Extract and show balance changes.
* Output values of the called smart contract function.
* Show events emitted during the simulated transaction execution.
* Display state changes.

The sample simulates the execution of an existing successful transaction sent to UniswapV2Router02 on the Ethereum Mainnet to retrieve additional information. Here's the transaction calling `swapExactTokensForTokens()`, exchanging 3,118.71 XCAD to USDT.

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

* Simulating the transaction on the block 16533181
* Simulating this transaction at a particular index within that block (in this case 1).
* Performing a [full simulation](simulation-api-quick-and-full-mode.md).

{% tabs %}
{% tab title="Request" %}
```typescript
import axios from 'axios';
import * as dotenv from 'dotenv';
dotenv.config();

// TX in question: https://dashboard.tenderly.co/nenad/observer/tx/mainnet/0xe165a7a77aa8973ff167f70b3ecb95cce6a6c5b1350e22176ed5c0784091daa4

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
      save: false, // if true simulation is saved and shows up in the dashboard
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
        '0x8803dbee00000000000000000000000000000000000000000000009df85158cbf910000000000000000000000000000000000000000000000000000000000000c65a511800000000000000000000000000000000000000000000000000000000000000a00000000000000000000000001cf5cd427d0a968379bd6b5befce28d8e157ae380000000000000000000000000000000000000000000000000000000063d9ac890000000000000000000000000000000000000000000000000000000000000002000000000000000000000000dac17f958d2ee523a2206206994597c13d831ec70000000000000000000000007659ce147d0e714454073a5dd7003544234b6aa0',
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
Simulated transaction info: hash: 0x57be7b9d6118a0fa3fc11fa9460d93cbec8e45a7ad1d6af501a6e0f02d1bf601 block number: 16527769
Balance changes 
  0x1cf5cd427d0a968379BD6b5BefcE28d8e157AE38: 178649986537506409 -> 175016718720819533 
  0xC0E1b256DE232262134c22f73b21F756072Bfb73: 4913764247259774380 -> 4913874657421732568 (Miner)
Output values
  amounts uint256[] = ["3282651314","2914031999999999475712"]
Events
  Transfer (from address = 0x1cf5cd427d0a968379bd6b5befce28d8e157ae38, to address = 0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a, value uint256 = 3282651314)
  Transfer (from address = 0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a, to address = 0x1cf5cd427d0a968379bd6b5befce28d8e157ae38, value uint256 = 2914031999999999475712)
  Sync (reserve0 uint112 = 254368076784473724455687, reserve1 uint112 = 288968153842)
  Swap (sender address = 0x7a250d5630b4cf539739df2c5dacb4c659f2488d, amount0In uint256 = 0, amount1In uint256 = 3282651314, amount0Out uint256 = 2914031999999999475712, amount1Out uint256 = 0, to address = 0x1cf5cd427d0a968379bd6b5befce28d8e157ae38)
State changes
  0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a
  reserve0: uint112
    "257282108784473723931399" -> "254368076784473724455687"
  
  0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a
  reserve1: uint112
    "285685502528" -> "288968153842"
  
  0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a
  blockTimestampLast: uint32
    1675166819 -> 1675179707
  
  0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a
  price0CumulativeLast: uint256
    "756643269219333625014234830491" -> "756717575180654871536825733691"
  
  0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a
  price1CumulativeLast: uint256
    "115330660026005862214326453602290190379962570339216427" -> "115390925201612227497765383158300036629651585476758491"
  
  0x7659ce147d0e714454073a5dd7003544234b6aa0
  _balances: mapping (address => uint256)
    {"0x1cf5cd427d0a968379bd6b5befce28d8e157ae38":"13735118200000000589824","0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a":"257282108784473723931399"} -> {"0x1cf5cd427d0a968379bd6b5befce28d8e157ae38":"16649150200000000065536","0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a":"254368076784473724455687"}
  
  0xdac17f958d2ee523a2206206994597c13d831ec7
  balances: mapping (address => uint256)
    {"0x1cf5cd427d0a968379bd6b5befce28d8e157ae38":"22963773121","0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a":"285685502528"} -> {"0x1cf5cd427d0a968379bd6b5befce28d8e157ae38":"19681121807","0x6f118ecebc31a5ffe49b87c47ea80f93a2af0a8a":"288968153842"}
  

```
{% endtab %}
{% endtabs %}
