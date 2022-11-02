# How to Simulate a Transaction

{% embed url="https://vimeo.com/639066114" %}

If you ever used the JSON-RPC, you've probably stumbled upon [eth\_call](https://github.com/ethereum/wiki/wiki/JSON-RPC#eth\_call). If you haven't, it returns you the output of a Smart Contract function, without submitting an on-chain transaction. This can be useful in some cases, but it is quite limited.

With the Simulate tool, you can **provide the data for a transaction and see what would happen if you submitted the transaction right now**. So you get all of the tools we already offer for on-chain transactions **for the pending block**.&#x20;

Not only that, but **you can even pick a specific block height, transaction index** and get the output of the transaction as if it happened at that specific point in time.

{% hint style="success" %}
Tenderly now automatically simulates the (expected) outcome of pending transactions when you paste the tx hash into the search bar, both in your [**Dashboard**](https://dashboard.tenderly.co/) and in our [**Public Explorer**](https://dashboard.tenderly.co/explorer).

This feature is available to all users, even if they are not logged in. That means that **you can now simulate live pending transactions** in this way even [**from our Explorer page**](https://dashboard.tenderly.co/explorer) without having an account - but you really should make one (it's free) so you can use the full power of our **Simulations** and **** [**Forks**](../how-to-create-a-fork/) 🚀

Read more about it [**here**](../../monitoring/contracts/mempool-and-simulating-pending-transactions.md).
{% endhint %}

### Starting a New Simulation

You can simulate any transaction on Tenderly in several ways. One of the easiest and probably most used ones would be to choose a desired on-chain transaction from the **Transactions** tab in the left navigation pane:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 17.00.15.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 17.00.34.png>)

In the top right you can see an option to **Re-Simulate** the transaction, which will launch the **Simulator** and allow you to change any and all [**transaction parameters**](transaction-parameters.md) **** before running the simulation:

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.50.15.png>)

You can also start the simulation by going to the **Simulator** tab in the left navigation pane and clicking on **New Simulation** in the top right, making it possible to run completely custom simulations:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 17.04.05.png>)

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.50.40.png>)

### Simulating a Transaction

So let's start up a new simulation with a public contract:

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 09.40.19.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 09.50.37.png>)

The simulated transaction will fail due to insufficient Dai balance:

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 09.50.56.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 09.51.46.png>)

You can immediately jump into the debugger and get to the line of code that caused the transaction to fail:

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 09.56.14.png>)

You can also change your contract source-code by clicking on Re-Simulate and then on Edit Contract Source ([**read more about this here**](editing-contract-source.md)):

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 09.58.46 (1).png>)

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 09.59.16 (1).png>)

The transaction failed again in a different place which was expected since we deleted a part of the code:

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 10.01.36.png>)

Clicking the back arrow or clicking on the **Simulator** tab in the left navigation pane brings you (back) to the historical list of all simulations:

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 10.19.02.png>)

You can [**modify various parameters in any Simulation**](transaction-parameters.md), such as **General Simulation Parameters**, **State Override** and **Optional Access List**.
