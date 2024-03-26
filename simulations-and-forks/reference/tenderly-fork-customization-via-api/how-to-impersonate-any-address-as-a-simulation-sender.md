---
description: Learn how to send a transaction from any address by running a simulation.
---

# How to Impersonate any Address as a Simulation Sender

In some scenarios, you may want to simulate transaction execution as if it was sent from an arbitrary address. When a transaction is simulated via API, Tenderly doesn’t deal with signatures, so you can set any `from` value. You can even simulate sending transactions from another contract.

To achieve this, just send a transaction with any `from` address:

```tsx
...
dotenv.config();
const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY, TENDERLY_FORK_ID } = process.env;

const SIMULATE_API = `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/fork/${TENDERLY_FORK_ID}/simulate`;

const provider = new ethers.providers.JsonRpcProvider(process.env.TENDERLY_FORK_URL);

const DAI_ADDRESS = "0x6b175474e89094c44da98b954eedeac495271d0f";

// DAI contract instance
const dai = ERC20__factory.connect(DAI_ADDRESS, provider);

const TX_DATA = await dai.populateTransaction[funcName](...args);

const transaction = {
    network_id: '1',
    from: "0x0000000000000000000000000000000000000000",
    input: TX_DATA.data,
    to: DAI_ADDRESS,
    block_number: null,
    // tenderly specific
    save: true
}

const opts = {
    headers: {
        "content-type": "application/JSON",
        'X-Access-Key': TENDERLY_ACCESS_KEY || "",
    }
}

try {
    const resp = await axios.post(SIMULATE_API, transaction, opts);
    console.log(resp.data);
} catch (err: any) {
    console.log(err.response.data.error);
}

```
