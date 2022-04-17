# Dry-run User Transactions

## Overview

Getting failed transactions is a kind of necessary evil when it comes to using dApps. But what if it doesn’t need to be?&#x20;

Here we are going to take a look at how to leverage Tenderly Simulations API to detect if a transaction would fail before you even send it on-chain.

Here are the steps to be taken in order to achieve this:

1. Populate raw transactions from ethers.js library.
2. Simulate transactions before sending them.
3. (optional) Wrap every blockchain interaction into a Tenderly Simulation.

### Populate raw transactions from ethers.js

The first step is to create a transaction object that is going to be sent to our simulation endpoint. We are going to generate it directly from the `ethers.js` library. In the example below we are going to see how we can achieve that for `transfer()` function on top of DAI contract:

```tsx
const dai = new ethers.Contract(DAI_ADDRESS , DAI_ABI , tenderlyForkProvider);

const unsignedTx = await dai.populateTransaction.transfer(ZERO_ADDRESS, YOUR_ADDRESS, util.ether(1));
```

### Simulate transactions before sending

Now that we have extracted an unsigned raw transaction, let's simulate it before sending it on-chain (to Ethereum Mainnet):

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

const headers = {
    headers: {
        'content-type': 'application/JSON',
        'X-Access-Key': TENDERLY_ACCESS_KEY,
  }
}
const resp = await axios.post(apiURL, body, headers);

if (resp.data.simulation.status === false) {
	// it failed, do as you please
}
```

### (optional) Wrap every blockchain interaction into Tenderly Simulation

In order to ensure that every blockchain interaction is simulated first, you can write a simple wrapper around the `ethers.js` signer object that would always simulate transactions.

Additionally, going forwards, you can introduce typed errors with which your logic can interact:

```tsx
export class TenderlySimulationSigner {
  public _provider: ethers.Provider;

  constructor(
    provider: ethers.Provider,
  ) {
    this._provider = provider;
  }

  public async sendTransaction(
    transaction: Deferrable<TransactionRequest>
  ): Promise<TransactionResponse> {
    await this._simulateTx(transaction)
		
    return this._signer.sendTransaction(transaction);
  }

  public async getAddress(): Promise<string> {
    return this._signer.getAddress();
  }

  public async signTransaction(
    transaction: Deferrable<TransactionRequest>
  ): Promise<string> {
    return this._signer.signTransaction(transaction);
  }

  _simulateTx(transaction: Deferrable<TransactionRequest>): Promise<void> {
    const unsignedTx = await contract.populateTransaction[funcName](...args)

    const apiURL = `https://api.tenderly.co/api/v1/account/me/project/project/simulate`
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

    const headers = {
        headers: {
            'content-type': 'application/JSON',
            'X-Access-Key': REACT_APP_TENDERLY_ACCESS_KEY as string,
      }
    }
    const resp = await axios.post(apiURL, body, headers);
    if (resp.data.simulation.status == false) {
        throw new Error("Transaction is going to fail")
    }

    return;
  }
}
```

{% hint style="success" %}
Here is the [link](https://github.com/Tenderly/integration-samples/tree/main/dry-run-transactions) to the GitHub repo where you can find an example of this implementation.
{% endhint %}
