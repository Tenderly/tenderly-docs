# Fork Parents

Fork Parents are a feature that allows for greater control over [**Simulations**](../how-to-simulate-a-transaction/) you run on your **Forks**, and much easier repeated testing of specific (historical) scenarios on your forked networks.&#x20;

For starters, we will [run a Fork Simulation](./) as we normally would. On the right under the section [**Transaction Parameters**](../how-to-simulate-a-transaction/transaction-parameters.md), you will have an option called `Parent` that will allow you to set the Parent for your Fork.&#x20;

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.24.51.png>)

The empty state for your Fork Parent if you don't have any branch roots defined is Latest Simulation. Naturally, in the Forks tab, you can **choose any of your previous Fork Simulations and mark it as a branch root** so you can use it as a Fork Parent in your Fork Simulations.

{% hint style="info" %}
Choosing `Latest Simulation` uses the parent ID from the Fork i.e. the latest transaction that happened on that Fork. If you just created a Fork, the last transaction will be defined as the last transaction in the block you forked the network from - this is neatly covered at the end of [creating a Fork section](./).



You can also [read more about Pending and Historical Blocks here.](../how-to-simulate-a-transaction/pending-vs-historical-block.md)
{% endhint %}

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.26.32.png>)

Marking your Fork Simulation as a branch root will add it to the list of Fork Parents you will be able to use going forward (and you can remove it as a branch root at any time).&#x20;

Branch roots will allow you to define any number of fixed points when forking networks so you can run Simulations from that or any other Parent.

You can also name your Fork Parents for easier navigation:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.27.44.png>)

Now, when you run a new Fork Simulation, you will see all of your Forks that were added as branch roots:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.28.37.png>)

All of the Fork Simulations that were ran with a Parent will be clearly marked:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.29.37.png>)

If you clear the branch root from a Fork the Parent column will be properly updated:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.30.11.png>)

If you mark a Fork as a branch root again after removing it, the Parent column will again be properly updated:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.31.21.png>)

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.31.41.png>)

You can also mark Forks as branch roots straight from the Transaction Overview tab:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.32.17.png>)
