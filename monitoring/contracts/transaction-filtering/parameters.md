# Parameters

What's better than having all transactions in one place? Filtering through them at the speed of light! Ok, maybe not the speed of light, but faster than anything else for sure:

![](../../../.gitbook/assets/image%20%2851%29.png)

As you can see, you can filter by multiple properties:

* **Transaction Status** - All/Success/Failed
* **Transaction Type** - All/Internal/Direct
* **Contracts** - Select which contracts must be present in the transaction
* **Network** - Specify the network if you have contracts deployed to multiple networks
* **Tag** - Filter by a specific tag that you provided during the **tenderly push** command \(more on this later\)

Having filtering this precise and fast is important when you need to pinpoint that specific transaction amongst thousands of them. Another example that comes to mind is finding internal transactions sent to your Smart Contracts that failed. This way, you can see if someone is trying to abuse your contract's logic or if your code is failing and someone depends on it.

