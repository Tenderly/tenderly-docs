---
description: >-
  Learn how to add a "transaction preview" option to the MetaMask wallet with
  the Tenderly Simulation API and give users a way to preview the outcome of
  their transactions before signing them.
---

# How to Add Transaction Preview to a MetaMask Snap Using Tenderly Simulation API

This tutorial demonstrates how to add a "transaction preview" option to a wallet using [Tenderly Simulation API](https://docs.tenderly.co/simulations-and-forks/simulation-api). We’ll show you how to add this option to the MetaMask wallet.

The "transaction preview" feature allows users to see the exact outcome of their transactions before submitting them to the production network. Wallets equipped with this feature make it easier for users to understand the financial implications of their transactions before making a commitment.

Simulations are executed on a fork of the latest state of the blockchain in a safe, risk-free environment. This helps wallet users prevent sending malicious or error-prone transactions.

You can find the complete demo repository on GitHub:

{% embed url="https://github.com/Tenderly/tenderly-metamask-snap-simulate-asset-changes" %}

{% embed url="https://youtu.be/DgfTifOM_V0" %}
Tenderly MetaMask Snap Demo
{% endembed %}

{% hint style="warning" %}
This tutorial is for demonstration purposes only, specifically to illustrate how to add a transaction preview option to a MetaMask Snap. It is not intended nor recommended for any other usage.
{% endhint %}

## Project overview

This project shows you how to integrate transaction simulations into the MetaMask wallet. We’ll be working with [MetaMask Snaps](https://metamask.io/snaps/).

You’ll learn how to connect to the [Tenderly Simulation API](https://docs.tenderly.co/simulations-and-forks/simulation-api), send the transaction data, retrieve the simulation results, and display them to the user via the MetaMask UI. This includes asset changes in dollars, native-asset balance changes, output value, storage changes, event logs, and call traces.

Simulated transactions can then also be opened in Tenderly for further debugging and testing.

Below is a list of features that we’ll be adding to the MetaMask Snap. Similar features can also be added to any wallet to help users build confidence when sending transactions.

| Feature                                     | Description                                                                                 |
| ------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Simulation debugging**                    | Auto-generated link to inspect and debug the simulation in Tenderly.                        |
| **Publicly sharable simulations**           | Ability to enable/disable public sharing of simulations.                                    |
| **Asset changes displayed in dollar value** | Human-readable data, including asset changes automatically converted into dollars           |
| **Native-asset balance changes**            | Ability to track changes in their native-asset balance during the execution of the contract |
| **Output value**                            | See the result of the contract call, displaying what the contract is set to return.         |
| **Storage changes**                         | See any changes made to the contract's storage during the execution                         |
| **Event logs**                              | See events that were emitted during the contract's execution                                |
| **Call traces**                             | Breakdown of all the function calls that happened during the execution                      |

### Prerequisites

* [MetaMask Flask](https://chrome.google.com/webstore/detail/metamask-flask-developmen/ljfoeinjpaedjfecbmggjgodbgkmjkjk) browser extension installed
* [Node.js](https://nodejs.org) (version 16 or later)
* [Yarn](https://classic.yarnpkg.com/lang/en/docs/install) (version 3)

{% hint style="info" %}
Before you start building the MetaMask Snap, make sure to disable the “real” version of MetaMask and [install the MetaMask Flask Development Plugin](https://chrome.google.com/webstore/detail/metamask-flask-developmen/ljfoeinjpaedjfecbmggjgodbgkmjkjk).
{% endhint %}

Let’s start building! 👷‍♂️

## Step 1: Setting up a MetaMask Snap project

Install MetaMask’s official [Create Snap CLI](https://docs.metamask.io/snaps/get-started/quickstart) and create a new project.

```bash
yarn create @metamask/snap project-name

OR 

npm create @metamask/snap project-name
```

Next, we need to start the Snap project and serve the front end on [https://localhost:8000](https://localhost:8000/).

From the root of the newly created project, install the project dependencies using Yarn.

```bash
yarn
```

Start the development server.

```bash
yarn start
```

### Setting the correct permissions

Once you’ve installed the Snap, find the `/packages/snap/snap.manifest.json` file and set the permissions as shown below. Learn about MetaMask permissions [here](https://docs.metamask.io/snaps/reference/permissions/).

```json
{
  // ...
  "initialPermissions": {
    "snap_dialog": {},
    "endowment:rpc": {
      "dapps": true,
      "snaps": false
    },
    "endowment:transaction-insight": {
      "allowTransactionOrigin": true
    },
    "endowment:network-access": {},
    "snap_manageState": {},
    "endowment:ethereum-provider": {
      "dapps": true,
      "snaps": true
    }
  }
}
```

When you run the app and try to connect the wallet, a permission request will pop up.

Click **Connect** and **Approve & install** buttons to continue.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption><p>Install MetaMask Snap Permissions</p></figcaption></figure>

## Step 2: Generating Tenderly API access tokens

The transaction preview option in the MetaMask Snap is powered by the Tenderly Simulation API.

Before you can start using the API, you need to generate access tokens. Follow these steps:

1. [Log into Tenderly or create a free account here](https://dashboard.tenderly.co/register).
2. Go to the [Authorization page](https://dashboard.tenderly.co/account/authorization) and click on the **Generate Access Token** button.

If you need help with API authentication, please follow this guide:

{% content-ref url="../../other/platform-access/how-to-generate-api-access-tokens.md" %}
[how-to-generate-api-access-tokens.md](../../other/platform-access/how-to-generate-api-access-tokens.md)
{% endcontent-ref %}

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Generate Access Token from Authorization page</p></figcaption></figure>

## Step 3: Writing the logic for the Snap

The core logic that makes the Snap work is stored in three files:

* **Credentials Access** (`credentials-access.ts`)**:** Manages the Tenderly API authentication and access.
* **Simulation** (`simulation.ts`)**:** The core logic for interacting with the Tenderly API to simulate transactions and fetch simulation results.
* **Formatter** (`formatter.ts`)**:** Logic for parsing simulation results and formatting them in a user-friendly way in the MetaMask UI.

### Credentials Access

We can store all methods responsible for requesting, updating, and fetching Tenderly API credentials in a file called **credentials-access.ts**. [View the source code here](https://github.com/Tenderly/tenderly-metamask-snap-simulate-asset-changes/blob/main/packages/snap/src/tenderly/credentials-access.ts).

The most important methods include:

* **`fetchCredentials()`**: This function retrieves the credentials of a Tenderly project. If no credentials are stored, it triggers `handleUpdateTenderlyCredentials` to request new ones.
* **`handleUpdateTenderlyCredentials()`**: This function handles the process of updating Tenderly project credentials. It gets new credentials by calling `requestNewTenderlyCredentials` and then saves them using the `snap_manageState` method with an `'update'` operation.
* **`requestNewTenderlyCredentials()`**: This function requests new Tenderly credentials. It calls `requestCredentials` to receive the raw credentials data and verifies its correctness before returning an object with `accountId`, `projectId`, and `accessToken`.

{% hint style="info" %}
**snap\_manageState** is a built-in method that allows the Snap to persist up to 100 MB of data to the disk. Learn more [here](https://docs.metamask.io/snaps/reference/rpc-api/#snap\_managestate).
{% endhint %}

### Simulation

Next, we need to create the logic that sends transaction data to the [Tenderly Simulation API](https://docs.tenderly.co/simulations-and-forks/simulation-api), simulates it, and retrieves the results.

We’ll use the **`simulate`** API endpoint for that.

```
https://api.tenderly.co/api/v1/account/{accountId}/project/{projectId}/simulate
```

To keep things organized, let’s store the simulation logic in a file called **simulation.ts**. [View the source code here.](https://github.com/Tenderly/tenderly-metamask-snap-simulate-asset-changes/blob/main/packages/snap/src/tenderly/simulation.ts)

To send transaction data to the Tenderly Simulation API, we need to create two key methods:

* **simulate()**: This is the main function that handles the simulation of a transaction. It fetches the API access credentials, submits the transaction data to the Tenderly Simulation API, and handles any errors returned by the API.

```tsx
export async function simulate(
  transaction: { [key: string]: Json },
  transactionOrigin: string,
): Promise<Panel> {
  const credentials = await fetchCredentials(transactionOrigin);

  if (!credentials) {
    return panel([text('🚨 Tenderly access token updated. Please try again.')]);
  }

  const simulationResponse = await submitSimulation(transaction, credentials);
  const err = catchError(simulationResponse, credentials);

  return err || formatResponse(simulationResponse, credentials);
}
```

* **submitSimulation()**: This function sends a request to the API along with the transaction data to be simulated.

When the transaction is simulated, we can make it publicly accessible by calling the share API endpoint. Making the simulation shareable allows you to copy the link to the transaction and send it to anyone. Shared transactions can be viewed without a Tenderly account.

```tsx
async function submitSimulation(
  transaction: { [key: string]: Json },
  credentials: TenderlyCredentials,
) {
  const chainId = await ethereum.request({ method: 'eth_chainId' });
  const response = await fetch(
    `https://api.tenderly.co/api/v1/account/${credentials.accountId}/project/${credentials.projectId}/simulate`,
    {
      method: 'POST',
      body: JSON.stringify({
        from: transaction.from,
        to: transaction.to,
        input: transaction.data,
        gas: hex2int(transaction.gas),
        value: hex2int(transaction.value),
        network_id: hex2int(chainId as string),
        save: true,
        save_if_fails: true,
        simulation_type: 'full',
        generate_access_list: false,
        source: 'tenderly-metamask-snap',
      }),
      headers: {
        'Content-Type': 'application/json',
        'X-Access-Key': credentials.accessToken,
      },
    },
  );

  const parsedResponse = await response.json();

  // Make the simulation publicly accessible
  if (parsedResponse?.simulation?.id) {
    await fetch(
      `https://api.tenderly.co/api/v1/account/${credentials.accountId}/project/${credentials.projectId}/simulations/${parsedResponse.simulation.id}/share`,
      {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
          'X-Access-Key': credentials.accessToken,
        },
      },
    );
  }

  return parsedResponse;
}
```

### Formatter

Once the API returns the simulation results, we need to parse this data and format it in a user-friendly way to be displayed in the MetaMask UI.

We can store this logic in a file called **formatter.ts**. [View the source code here.](https://github.com/Tenderly/tenderly-metamask-snap-simulate-asset-changes/blob/main/packages/snap/src/tenderly/formatter.ts)

The core formatting methods include:

* **`formatResponse()`**: This function receives the raw data and credentials of a Tenderly project simulation, calls the individual formatter functions for each relevant section (like balance changes, output value, asset changes, etc.), and returns a panel with all the formatted outputs.
* **`formatBalanceDiff()`**: This function generates a panel showing balance changes for each account involved in the transaction.
* **`formatOutputValue()`**: This function creates a panel that presents the output values of the transaction if any exist. It also decodes the output, if possible.
* **`formatAssetChanges()`**: This function formats a panel to show any asset changes, differentiating between ERC20, ERC721, and other changes.
* **`formatStorageChanges()`**: This function creates a panel that lists any changes to storage that occurred during the transaction. It uniquely formats addresses and nested data structures for clarity.
* **`formatEventLogs()`**: This function presents the event logs, if they exist, for each transaction. The logs are formatted for readability and include input values.
* **`formatCallTrace()`**: This function produces a formatted visual hierarchy of call traces, showing nested calls recursively.
* **`formatSimulationUrl()`**: This function returns a link to the full details of the simulation on the Tenderly Dashboard and a separate shareable link.

## Step 4: Displaying simulation data in the MetaMask UI

The [MetaMask Snap mono repo](https://github.com/MetaMask/template-snap-monorepo) provides a set of predefined UI elements and layout configurations. We'll use these elements to extend the existing MetaMask UI to display the simulation results.

When you install our MetaMask example, we show you how to run different types of simulations:

* **Successful transaction simulation** with a predefined payload (successful ERC-20 transfer and NFT transfer)
* **Failed transaction simulation** with a predefined payload
* **Custom transaction simulation** with any payload

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Tenderly Snap UI</p></figcaption></figure>

For the purpose of this tutorial, we’ll show you how to run simulations with a predefined payload and how to add your custom payload and execute the simulation.

### Successful simulation with a predefined payload

To initiate a simulation, we’ll write a function that will send the predefined transaction data from our wallet address and call the `eth_sendTransaction` RPC method.

```tsx
// packages/site/src/utils/snap.ts

export const sendTransaction = async (data: any): Promise<any> => {
  try {
    const [from] = (await window.ethereum.request({
      method: 'eth_requestAccounts',
    })) as string[];

    if (!from) {
      return Promise.reject(Error('Failed to get an account'));
    }

    // https://ethereum.org/en/developers/docs/apis/json-rpc/#eth_sendtransaction
    return window.ethereum.request({
      method: 'eth_sendTransaction',
      params: [
        {
          ...data,
          from,
        },
      ],
    });
  } catch (e) {
    console.error(e);
    return e;
  }
};
```

The `eth_sendTransaction` method call will trigger the `onTransaction` handler, which will call our custom `simulate` function, which was defined in `simulation.ts`.

```tsx
// packages/snap/src/index.ts

export const onTransaction: OnTransactionHandler = async ({
  transaction,
  transactionOrigin,
}) => {
  if (!isObject(transaction) || !hasProperty(transaction, 'to')) {
    return {
      content: {
        value: 'Unknown transaction type',
        type: NodeType.Text,
      },
    };
  }

  const simulationResponse = await simulate(
    transaction,
    transactionOrigin || '',
  );

  return {
    content: {
      children: simulationResponse.children,
      type: NodeType.Panel,
    },
  };
};
```

In the `onTransaction` handler, the `simulate` function is called with the transaction and its origin as arguments.

The `simulate` function is responsible for fetching access credentials, submitting the transaction data to the Tenderly API, handling any errors, and formatting the API response for output.

The results of the simulation are displayed within the MetaMask UI. The images below show a successful ERC20 token transfer of 1 USDC to `demo.eth`. The output is generated by the functions defined in the `formatter.ts` file.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>ERC20 Transfer - send 1 USDC to demo.eth</p></figcaption></figure>

For example, the **Asset Changes** block, which shows us the dollar value changes resulting from the simulation, is generated by the `formatAssetChanges()` function.

You also get a link to the simulated transaction which you can open in Tenderly and inspect it further with [Debugger](../../debugger/how-to-use-tenderly-debugger/) or resimulate it with different values.

This link is generated by the `formatSimulationUrl()` function defined in the `formatter.ts` file.

```typescript
export function formatSimulationUrl(
  data: any,
  credentials: TenderlyCredentials,
): Component[] {
  const simulationUrl = `https://dashboard.tenderly.co/${credentials.accountId}/${credentials.projectId}/simulator/${data.simulation?.id}`;
  const sharedSimulationUrl = `https://dashboard.tenderly.co/shared/simulation/${data.simulation?.id}`;

  return [
    heading('Tenderly Dashboard:'),
    text('See full simulation details in Tenderly.'),
    text(
      `**Status:** ${data.transaction?.status ? 'Success ✅' : 'Failed ❌'}`,
    ),
    copyable(`${simulationUrl}`),
    text('Share simulation details with others! 🤗'),
    copyable(`${sharedSimulationUrl}`),
  ];
}
```

### Failed transaction with a predefined payload

For the second example, we’ll simulate a failed transaction with a predefined payload.

The image below shows a failed ERC20 token transfer of 1,000,000 USDC to `demo.eth`.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Preview of the failed transaction</p></figcaption></figure>

We also get a link to the Tenderly Dashboard, where the user can inspect the stack trace, events, state changes, gas consumption, etc. This is particularly useful for understanding why the transaction failed.

The user can smoothly continue debugging the failed transaction and resimulating it to test different solutions.

### Simulation with a custom payload

To run a simulation with a custom payload, you need to add an object that aligns with the [Ethereum transaction specification](https://ethereum.org/en/developers/docs/apis/json-rpc/#eth\_sendtransaction).

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption><p>Custom payload UI</p></figcaption></figure>

It can contain the following fields:

* `from`: `DATA`, 20 Bytes - The address the transaction is sent from.
* `to`: `DATA`, 20 Bytes - (optional when creating a new contract) The address the transaction is directed to.
* `gas`: `QUANTITY` - (optional, default: 90000) Integer of the gas provided for the transaction execution. It will return unused gas.
* `gasPrice`: `QUANTITY` - (optional, default: To-Be-Determined) Integer of the gasPrice used for each paid gas.
* `value`: `QUANTITY` - (optional) Integer of the value sent with this transaction.
* `data`: `DATA` - The compiled code of a contract OR the hash of the invoked method signature and encoded parameters.
* `nonce`: `QUANTITY` - (optional) Integer of a nonce. This allows you to overwrite your own pending transactions that use the same nonce.

All numerical values should be hexadecimal strings, and addresses should be Ethereum addresses (20 bytes).

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Send a custom payload</p></figcaption></figure>

After entering the custom payload, users can initiate the simulation using the same `sendTransaction` function as before. This passes the custom payload to the `onTransaction` handler, which then triggers the `simulate` function to run the simulation.

## Next steps

In this tutorial, you learned how to add a transaction preview option to a MetaMask Snap powered by the Tenderly Simulation API. You can find the [source code for this project on GitHub](https://github.com/Tenderly/tenderly-metamask-snap-simulate-asset-changes).

Transaction simulation on Tenderly can be initiated in three ways, depending on your project and needs. Learn how to integrate simulations into your dapps with these help resources:

{% content-ref url="../how-to-simulate-a-transaction/" %}
[how-to-simulate-a-transaction](../how-to-simulate-a-transaction/)
{% endcontent-ref %}

{% content-ref url="../simulation-api/" %}
[simulation-api](../simulation-api/)
{% endcontent-ref %}

{% content-ref url="../simulation-rpc.md" %}
[simulation-rpc.md](../simulation-rpc.md)
{% endcontent-ref %}
