# How to Simulate a Transaction

If you ever used the JSON-RPC, you've probably stumbled upon [eth\_call](https://github.com/ethereum/wiki/wiki/JSON-RPC#eth_call). If you haven't, it returns you the output of a Smart Contract function, without submitting an on-chain transaction. This can be useful in some cases, but it is quite limited.

With the Simulate tool, you can **provide the data for a transaction and see what would happen if you submitted the transaction right now**. So you get all of the tools we already offer for on-chain transactions **for the pending block**. 

Not only that, but **you can even pick a specific block height, transaction index** and get the output of the transaction as if it happened at that specific point in time.

{% embed url="https://vimeo.com/397986714" %}



