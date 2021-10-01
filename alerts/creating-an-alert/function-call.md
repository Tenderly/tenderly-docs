# Function Call

{% embed url="https://www.loom.com/share/20a4be09bdfd4843b0ef9c64fd8b67cb" %}

#### Introduction

Triggers whenever a specific function is called in one of your contracts. Receive an alert not only when a function is first called in a transaction, but each time it is called during the execution of a transaction.

#### Example 1

Let’s get notified every time a new CryptoKitty is born.

* First of all, we need to add the CryptoKitties contract to Project. _CryptoKitties Smart Contract address is 0x06012c8cf97bead5deae237070f9587f8e7a266d_. You can see here how to **\[Add new contract\]** into Project. 
* Click on **Alerting** in the navigation **—&gt;** **New Alert** **—&gt;** **Function Call —&gt; Contract —&gt; Select Contract —&gt;**Find **KittyCore** Smart Contract and Choose it **—&gt;** Choose **giveBirth** function **—&gt; Next —&gt;** Choose Alert Destination **—&gt; Save.** 
* That’s it! You’ll get a notification whenever a cute little CryptoKitty comes into this world. Or not this world, but to the Ethereum blockchain at least. 
* When Alert was created if we want to add a description, alert level, more alert destinations, or change the name, we can do that. You can see how in [Edit Alert](editing-an-alert.md).

#### Example 2

Another great example is that sometimes we want to get alerted when a specific function was called in a transaction. And no, we're not talking about just the first function that was called in a transaction - we're talking about getting notified if that specific function was called at any time during the execution of a transaction.

Let’s get notified every time a new CryptoKitty is born:

* I’m going to add the CryptoKitties Smart Contract to my project by importing it from Etherscan by going to my project, then click on Add Contract and paste in the following address: **0x06012c8cf97bead5deae237070f9587f8e7a266d** 
* Go to the alerts tab and select the **Function Call** rule
* Pick the **KittyCore** Smart Contract as the Alert target
* Select the **giveBirth** function

![](../../.gitbook/assets/image%20%2867%29.png)

That’s it! You’ll get an e-mail whenever a cute little CryptoKitty comes into this world. Or not this world, but to the Ethereum blockchain at least.

