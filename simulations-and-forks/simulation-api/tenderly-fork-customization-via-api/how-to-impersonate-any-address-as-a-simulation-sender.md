# How to Impersonate any Address as a Simulation Sender

In some scenarios, you may want to simulate the transaction execution as if it was sent from an arbitrary address, even though in the real world you couldn’t. When a transaction is simulated via API, Tenderly doesn’t deal with signatures, so you can set any `from` value - you can even simulate sending transactions from another contract.

The way to achieve this is not as complicated, just send a transaction with any from address:

```tsx
...
dotenv.config();
const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;

const SIMULATE_API = `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/simulate`

const DAI_ADDRESS = "0x6b175474e89094c44da98b954eedeac495271d0f";

// tx data obtained using other means
const TX_DATA = const unsignedTx = await contract.populateTransaction[funcName](...args);

const transaction = {
    network_id: '1',
    from: "0x0000000000000000000000000000000000000000",
    input: TX_DATA,
    to: DAI_ADDRESS,
    block_number: null,
    // tenderly specific
    save: true
}

const opts = {
    headers: {
        'X-Access-Key': process.env.TENDERLY_ACCESS_KEY || "",
    }
}
const resp = await axios.post(SIMULATE_API, transaction, opts);
console.log(resp.data);
```
