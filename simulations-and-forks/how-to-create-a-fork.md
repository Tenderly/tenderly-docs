# How to Create a Fork

{% hint style="success" %}
Forks allow you to chain [**Simulations**](how-to-simulate-a-transaction/) and test out complex scenarios with live on-chain data.
{% endhint %}

Let's start up a new Fork:

![](<../.gitbook/assets/Screenshot 2021-10-15 at 10.22.17.png>)

Choose the network you want to fork and name it:

![](<../.gitbook/assets/Screenshot 2021-10-15 at 10.23.24.png>)

![](<../.gitbook/assets/Screenshot 2021-10-15 at 10.24.00.png>)

You can choose the block from which you want to fork the chosen network, either latest or historical ([**read more about that here**](how-to-simulate-a-transaction/pending-vs-historical-block.md)):

![](<../.gitbook/assets/Screenshot 2021-10-15 at 10.25.01.png>)

Regardless of the chosen block, we can now create a Simulation on our newly created Fork:

![](<../.gitbook/assets/Screenshot 2021-10-15 at 10.27.32.png>)

![](<../.gitbook/assets/Screenshot 2021-10-15 at 10.35.01.png>)

You can use either public or [**custom contracts**](how-to-simulate-a-transaction/transaction-parameters.md) here as well:

![](<../.gitbook/assets/Screenshot 2021-10-15 at 10.39.25.png>)

All that is left to do is fill out the fork simulation parameters, click **Simulate Transaction** and that's it - you can now run as many simulations as you want on your fork!



#### A few important notes to be aware of when using the Forks feature:

{% hint style="warning" %}
When you are creating a **Fork** from the **block number N**, the **Simulations** you run on that Fork **will run in block number N and not N + 1**.&#x20;

This means that your Fork, when created, has all the state from block number N-1, and not N.
{% endhint %}

{% hint style="info" %}
Each **Simulation** you do on your **Fork** going forwards will be placed in a separate block, regardless of using the [**Historical** or the **Pending block**](how-to-simulate-a-transaction/pending-vs-historical-block.md) option.
{% endhint %}
