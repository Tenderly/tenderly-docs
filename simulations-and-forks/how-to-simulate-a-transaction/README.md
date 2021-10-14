# How to Simulate a Transaction

If you ever used the JSON-RPC, you've probably stumbled upon [eth_call](https://github.com/ethereum/wiki/wiki/JSON-RPC#eth_call). If you haven't, it returns you the output of a Smart Contract function, without submitting an on-chain transaction. This can be useful in some cases, but it is quite limited.

With the Simulate tool, you can **provide the data for a transaction and see what would happen if you submitted the transaction right now**. So you get all of the tools we already offer for on-chain transactions **for the pending block**. 

Not only that, but **you can even pick a specific block height, transaction index** and get the output of the transaction as if it happened at that specific point in time.

{% embed url="https://vimeo.com/397986714" %}

## Simulating a Transaction

You can simulate any transaction on Tenderly in several ways. One of the easiest and probably most used ones would be to choose a desired on-chain transaction from the **Transactions **tab in the left navigation pane:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 17.00.15.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 17.00.34.png>)

In the top right you can see an option to **Re-Simulate **the transaction, which will launch the **Simulator** and allow you to change any and all [**transaction parameters**](transaction-parameters.md)** **before running the simulation:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 17.01.18.png>)

You can also start the simulation by going to the **Simulator **tab in the left navigation pane and clicking on **New Simulation** in the top right, making it possible to run completely custom simulations:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 17.04.05.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 17.06.07.png>)

