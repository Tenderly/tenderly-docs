# Mempool & Simulating Pending Transactions

### Exploring Mempool and Filtering Pending Transactions

When exploring the transaction list in the **Transactions** tab (on the left), you can filter the default view and see **Pending Transactions** from the **mempool** as well - either by clicking the checkbox at the top or by clicking on Filter Transactions button in the top right.

![](<../../.gitbook/assets/Screenshot 2022-01-25 at 12.21.02.png>)

![](<../../.gitbook/assets/Screenshot 2022-01-25 at 12.22.32.png>)

When you click on and open a pending transaction, the expected outcome will be automatically simulated using the most recent state.

![](<../../.gitbook/assets/Screenshot 2022-01-25 at 12.24.02.png>)

### Simulating Pending Transactions

When you search for a transaction which is not yet mined and cannot be found in the system, **Tenderly will retrieve said transaction directly from the node pending pool and Simulate it using the most recent state**.

![Simulated Pending Transaction - Failed](<../../.gitbook/assets/Screenshot 2021-11-25 at 11.12.56.png>)

![Simulated Pending Transaction - Successful](<../../.gitbook/assets/Screenshot 2021-11-25 at 11.23.42.png>)

This means that you can **see the expected outcome of your or any other transaction** even before it is approved on the Mainnet.

{% hint style="success" %}
This feature is available to all users, even if they are not logged in. That means that **you can simulate pending transactions** in this way even [**from our Explorer page**](https://dashboard.tenderly.co/explorer) without having an account - but you really should make one (it's free) so you can use the full power of our [**Simulations**](../../simulations-and-forks/how-to-simulate-a-transaction/) and [**Forks**](broken-reference) 🚀
{% endhint %}
