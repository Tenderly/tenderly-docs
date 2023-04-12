---
description: >-
  With the Tenderly SDK, you can simulate individual transactions or bundles of
  transactions, manage contracts and wallets, and verify contracts from your
  code.
---

# Intro to Tenderly SDK

The Tenderly SDK is a TypeScript library that provides a set of useful utilities, enabling you to move faster through the different development stages using Tenderly.&#x20;

It allows you to simulate transactions, simulate transaction bundles, manage contracts and wallets, and verify smart contracts from your code. The SDK is particularly useful for blockchain developers who want to integrate Tenderly's powerful tools into their dapp or development workflow.

### **Introduction**

The Tenderly SDK provides an easy-to-use interface for interacting with the Tenderly platform via API.

**Key features of the SDK include:**

* [Simulating transactions](simulating-transactions.md)
* [Managing and verifying contracts](managing-contracts.md)
* [Managing wallets](managing-wallets.md)

### **Installation**

The Tenderly SDK is available as an [npm package](https://www.npmjs.com/package/@tenderly/sdk). Install it by running the following command in your project directory:

**npm**

```bash
npm install @tenderly/sdk
```

**yarn**

```bash
yarn add @tenderly/sdk
```

**pnpm**

```bash
pnpm add @tenderly/sdk
```

### Quickstart

The example below shows you how to do a simple simulation in less than 5 minutes. To learn more about the concepts behind the SDK, see [Tenderly SDK FAQs](basic-concepts-and-faqs.md).

#### **Initializing the SDK**

To use the Tenderly SDK, you must first import the necessary libraries and create a new instance of the **`Tenderly`** class. This is where you pass in your Tenderly configuration details.

The configuration object should include your account name, project name, access key, and network.

```jsx

import { Tenderly, Network } from "@tenderly/sdk";

const tenderlyInstance = new TenderlyInstance({
  accountName: "my-account",
  projectName: "my-project",
  accessKey: "my-access-key",
  network: Network.MAINNET, // Replace with the appropriate network
});
```

If you don’t want to hardcode sensitive information like API keys, you can use environment variables to store this information, like so:

```jsx
import { Tenderly, Network } from '@tenderly/sdk';

const tenderlyInstance = new TenderlyInstance({
  accountName: process.env.TENDERLY_ACCOUNT_NAME,
  projectName: process.env.TENDERLY_PROJECT_NAME,
  accessKey: process.env.TENDERLY_ACCESS_KEY,
  network: Network.MAINNET, // Replace with the appropriate network
});
```

{% hint style="info" %}
The list of [supported networks](https://docs.tenderly.co/supported-networks-and-languages) can be found here.
{% endhint %}

#### How to get the account name, project slug, and secret key

Follow these step-by-step guides to obtain the necessary configuration details:

* [How to obtain the account name](https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name#username)
* [How to obtain the organization name](https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name#organization-name)
* [How to obtain the project slug/name](https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name#project-name-or-slug)
* [How to find, create, and manage API keys](https://docs.tenderly.co/other/platform-access/how-to-generate-api-access-tokens)

### **Example transaction simulation**

The SDK provides a **`Simulator`** class for simulating transactions. To run a simulation, call the **`simulateTransaction`** method in the **`simulator`** namespace on the Tenderly instance:

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

The code above produces the following result:

```json
{
  status: true,
  gasUsed: '46838',
  cumulativeGasUsed: undefined,
  blockNumber: '3237677',
  type: undefined,
  logsBloom: 'AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAIAAAAAAAAAAAAAAAAAAAAAAAACAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAAAAAAAAAA==',
  logs: [ { raw: [Object] } ],
  trace: [
    {
      type: 'CALL',
      from: '0xDBcB6Db1FFEaA10cd157F985a8543261250eFA46',
      to: '0x93Cc0A80DE37EC4A4F97240B9807CDdfB4a19fB1',
      gas: '19978936',
      gas_used: '25774',
      value: '0',
      input: '0x371303c0',
      trace_address: [Array]
    }
  ]
}
```

### Next steps

For more guidance on running simulations with the Tenderly SDK, give these tutorials a go and learn how to simulate both individual and bundled transactions.

{% content-ref url="tutorials-and-quickstarts/how-to-simulate-transactions-with-tenderly-sdk.md" %}
[how-to-simulate-transactions-with-tenderly-sdk.md](tutorials-and-quickstarts/how-to-simulate-transactions-with-tenderly-sdk.md)
{% endcontent-ref %}

{% content-ref url="tutorials-and-quickstarts/how-to-perform-simulation-bundles-with-tenderly-sdk.md" %}
[how-to-perform-simulation-bundles-with-tenderly-sdk.md](tutorials-and-quickstarts/how-to-perform-simulation-bundles-with-tenderly-sdk.md)
{% endcontent-ref %}

And as you continue learning how the Tenderly SDK works, we recommend taking at look at these helpful resources:

ℹ️[ How to manage and verify smart contracts ](managing-contracts.md)

ℹ️ [How to manage wallets](managing-wallets.md)

ℹ️[ ](basic-concepts-and-faqs.md)[Practical examples and code snippets](practical-examples.md)

ℹ️[ SDK basic concepts](basic-concepts-and-faqs.md)
