---
description: >-
  Learn more about Fork Parents and how to use this functionality to establish
  greater control over running simulations on a Fork.
---

# Fork Parents

Fork Parents are a feature that allows for greater control over the simulations you run on a **Fork**. This functionality facilitates repeated testing of specific (historical) scenarios on your forked networks.&#x20;

### Run a simulation on a Fork&#x20;

First, [run a simulation on your Fork](broken-reference) as you normally would. On the right under the [Transaction Parameters](../how-to-simulate-a-transaction/transaction-parameters.md) section, you have an option called `Parent` that allows you to set the Parent for your Fork.&#x20;

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.24.51.png>)

### Set the Fork Parent

Branch roots allow you to define any number of fixed points when forking networks so you can run simulations from that or any other Parent. If you don't have any branch root defined, the empty state for your Fork Parent is Latest Simulation.&#x20;

To set a specific branch root, choose any of your previous Fork simulations in the Forks tab and mark it as a branch root. This way, you can use a specific simulation as a Fork Parent in your Fork simulations.

{% hint style="info" %}
Choosing `Latest Simulation` uses the parent ID from the Fork i.e. the latest transaction that happened on that Fork. If you just created a Fork, the last transaction will be defined as the last transaction in the block you forked the network from.&#x20;

You can also [learn more about pending and historical blocks.](../how-to-simulate-a-transaction/pending-vs-historical-block.md)
{% endhint %}

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.26.32.png>)

Marking a specific simulation on your Fork as a branch root adds it to the list of Fork Parents you can use going forward. You can remove it as a branch root at any time.&#x20;

You can also name your Fork Parents for easier navigation:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.27.44.png>)

### Use a Fork Parent

Now, when you run a new Fork simulation, you'll see all of your Forks that you added as branch roots:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.28.37.png>)

All of the Fork simulations executed with a Parent are clearly marked:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.29.37.png>)

If you clear the branch root from a Fork, the Parent column will be properly updated:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.30.11.png>)

You can mark a Fork as a branch root again after removing it:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.31.21.png>)

The Parent column will again be properly updated:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.31.41.png>)

You can also mark Forks as branch roots straight from the Transaction Overview tab:

![](<../../.gitbook/assets/Screenshot 2021-11-12 at 10.32.17.png>)
