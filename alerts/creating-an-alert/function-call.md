# Function Call

Another great example is that sometimes we want to get alerted when a specific function was called in a transaction. And no, we're not talking about just the first function that was called in a transaction - we're talking about getting notified if that specific function was called at any time during the execution of a transaction.

Let’s get notified every time a new CryptoKitty is born:

* I’m going to add the CryptoKitties Smart Contract to my project by importing it from Etherscan by going to my project, then click on Add Contract and paste in the following address: **0x06012c8cf97bead5deae237070f9587f8e7a266d** 
* Go to the alerts tab and select the **Function Call** rule
* Pick the **KittyCore** Smart Contract as the Alert target
* Select the **giveBirth** function

![](../../.gitbook/assets/image%20%2857%29.png)

That’s it! You’ll get an e-mail whenever a cute little CryptoKitty comes into this world. Or not this world, but to the Ethereum blockchain at least.

