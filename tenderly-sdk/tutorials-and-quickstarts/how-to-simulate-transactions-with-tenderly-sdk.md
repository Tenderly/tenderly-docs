---
description: Learn how to execute a simple transaction simulation using the Tenderly SDK.
---

# How to Simulate Transactions with Tenderly SDK

In this tutorial, you'll learn how to run a transaction simulation using the Tenderly SDK. Simulations allow you to test the behavior of your transactions without sending them on-chain. Learn more about Tenderly's [Transaction Simulator here](https://docs.tenderly.co/simulations-and-forks/intro-to-simulations).&#x20;

### **Prerequisites**

* Node.js installed on your machine
* [Tenderly account with an API key](../../other/platform-access/how-to-generate-api-access-tokens.md)
* [Project set up in the Tenderly Dashboard](https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name)

{% hint style="success" %}
Use this link to [sign up for Tenderly](https://dashboard.tenderly.co/register?utm\_source=homepage).&#x20;
{% endhint %}

### **Step 1: Initialize a new Node.js project**

Create a new directory for your project, navigate to it in the terminal, and initialize a new Node.js project:

```bash
mkdir tenderly-simulation
cd tenderly-simulation
npm init -y

```

### **Step 2: Install Tenderly SDK**

Install the [Tenderly SDK npm package ](https://www.npmjs.com/package/@tenderly/sdk)as a dependency in your Node.js project:

```bash
npm install @tenderly/sdk
```

### **Step 3: Import the Tenderly SDK and configure it**

Create a new file named **`index.js`** in your project directory, and add the following code to import the Tenderly SDK and configure it with your Tenderly account details:

```jsx
const { Tenderly, Network } = require("@tenderly/sdk");

const tenderly = new Tenderly({
  accountName: "your-account-name",
  projectName: "your-project-name",
  accessKey: "your-access-key",
  network: Network.MAINNET, // Replace with the appropriate network
});

```

Make sure to replace **`your-account-name`**, **`your-project-name`**, and **`your-access-key`** with your actual Tenderly account information.

{% hint style="info" %}
Follow these guides to [obtain the configuration details](../intro-to-tenderly-sdk.md#how-to-get-the-account-name-project-slug-and-secret-key).
{% endhint %}

### **Step 4: Define the transaction details**

Next, define the transaction details for the simulation.&#x20;

Add the following code to **`index.js`**:

```jsx
const transactionParameters = {
  from: "0x742d35Cc6634C0532925a3b844Bc454e4438f44e",
  to: "0x742d35Cc6634C0532925a3b844Bc454e4438f44f",
  input: "0x606060...",
  value: "1000000000000000000",
  gas: 21000,
  gas_price: "20000000000",
};

const simulationDetails = {
  transaction: transactionParameters,
  blockNumber: 12000000,
  override: {}, // Optional state override
};

```

Replace the **`from`**, **`to`**, **`input`**, **`value`**, **`gas`**, and **`gas_price`** fields with your desired transaction details. The **`override`** field is optional and allows you to override the state of specific contracts in the simulation.

{% hint style="warning" %}
Make sure that the specified block number actually exists on the selected network.
{% endhint %}

### **Step 5: Run the transaction simulation**

Now, use the Tenderly SDK's **`simulateTransaction`** method to run the transaction simulation.&#x20;

Add the following code to **`index.js`**:

```jsx
(async () => {
  try {
    const simulationResult = await tenderly.simulator.simulateTransaction(simulationDetails);
    console.log("Simulation result:", simulationResult);
  } catch (error) {
    console.error("Error running simulation:", error);
  }
})();

```

This code runs an asynchronous function that calls the **`simulateTransaction`** method and logs the simulation result to the console.

### **Step 6: Execute the script**

Save the **`index.js`** file and run the script using the following command:

```jsx
node index.js
```

If the transaction simulation is successful, you'll see the simulation result printed in the console.

That's it! You've now learned how to run a transaction simulation using the Tenderly SDK.
