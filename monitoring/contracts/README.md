# Transaction Overview

When you enter your project, the first thing that you see is the **Transactions** tab:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 15.16.56.png>)

Here you can find the list of all of the transactions that include any of your Smart Contracts. **Yes, that means both direct and internal transactions**.

We also backfill all of the transactions that happened before you added your Smart Contracts to Tenderly.

You can also choose which columns will be shown on the transaction overview screen:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 15.16.23.png>)

From this page you can do several things - explore the [**Execution Overview**](execution-overview.md) to see everything that happened in the transaction, jump into the [**Debugger**](../../debugger/how-to-use-tenderly-debugger/) for more a more in-depth look, or even start up a [**Simulation**](../../simulations-and-forks/how-to-simulate-a-transaction/) (or a [**Fork**](../../simulations-and-forks/how-to-create-a-fork/)) for you to experiment and test the outcomes of the transaction by changing any and all of its parameters.

## Transaction Filtering

What's better than having all transactions in one place? Filtering through them at the speed of light! Ok, maybe not the speed of light, but faster than anything else for sure.

In the **Transactions** tab in the left navigation we have an option to filter transactions according to several parameters:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 15.08.19.png>)

* Status - All/Success/Failed
* Type - All/Internal/Direct
* Contracts (now **Addresses**) - select which address (for a contract or a wallet) must be present in the transaction
* Function Signature
* Network - specify the network if you have contracts deployed to multiple networks
* Date Range
* Tag

![](<../../.gitbook/assets/image (70) (1) (1).png>)

There is also an option, after you select a tag to filter by, to show only transactions that happened after a certain tag was created:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 15.10.19.png>)

Having filtering this precise and fast is important when you need to pinpoint that specific transaction amongst thousands of them. Another example that comes to mind is finding internal transactions sent to your Smart Contracts that failed. This way, you can see if someone is trying to abuse your contract's logic or if your code is failing and someone depends on it.

{% hint style="success" %}
Tenderly now automatically simulates the (expected) outcome of pending transactions when you paste the tx hash into the search bar, both in your [**Dashboard**](https://dashboard.tenderly.co/) and in our [**Public Explorer**](https://dashboard.tenderly.co/explorer).

This feature is available to all users, even if they are not logged in. That means that **you can now simulate live pending transactions** in this way even [**from our Explorer page**](https://dashboard.tenderly.co/explorer) without having an account - but you really should make one (it's free) so you can use the full power of our [**Simulations**](../../simulations-and-forks/how-to-simulate-a-transaction/) **** and **** [**Forks**](../../simulations-and-forks/how-to-create-a-fork/) 🚀

Read more about it [**here**](mempool-and-simulating-pending-transactions.md).
{% endhint %}

## Advanced Trace Search

When you look at the Execution Trace segment of the Transaction Overview for any transaction, you will see this button next to the Execution Search which opens the Advanced Trace Search:

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 14.36.13.png>)

You will be able to search for a trace by following categories:

* All (all listed categories will be searched)
* OpCode
* From
* To
* Function
* File
* Contract
* State Variable

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 14.38.05.png>)

![](<../../.gitbook/assets/Screenshot 2022-03-16 at 14.19.29.png>)

When you click on any of the search results, you will be taken to the corresponding line of code in the Execution Trace segment:

![](<../../.gitbook/assets/Screenshot 2022-03-16 at 14.20.16.png>)
