---
description: >-
  Use these code snippet examples to execute individual and bundled transactions
  using the Tenderly SDK.
---

# Simulating Transactions

The SDK provides a **`Simulator`** class for simulating transactions. To run a simulation, call the **`simulateTransaction`** method in the **`simulator`** namespace on the **`tenderly`** instance:

```jsx
const transaction = await tenderly.simulator.simulateTransaction({
    transaction: {
      from: callerAddress,
      to: counterContract,
      gas: 20000000,
      gas_price: '19419609232',
      value: 0,
      input: counterContractAbiInterface.encodeFunctionData('inc', []),
    },
    blockNumber: 3237677,
  });
```

You can also simulate a bundle of transactions by calling the **`simulateBundle`** method:

```javascript
const simulations = await tenderly.simulator.simulateBundle({
      transactions: [
        {
          from: fromWalletAddress,
          to: myTokenAddress,
          gas: 0,
          gas_price: '0',
          value: 0,
          input: myTokenAbiInterface.encodeFunctionData('approve', [toWalletAddress, 1234567890]),
        },
        {
          from: toWalletAddress,
          to: myTokenAddress,
          gas: 0,
          gas_price: '0',
          value: 0,
          input: myTokenAbiInterface.encodeFunctionData('transferFrom', [
            fromWalletAddress,
            toWalletAddress,
            1234567890,
          ]),
        },
      ],
      blockNumber: 3262454,
      overrides: {
        [myTokenAddress]: {
          state: {
            [`_balances[${fromWalletAddress}]`]: '1234567891',
          },
        },
      },
    });
```
