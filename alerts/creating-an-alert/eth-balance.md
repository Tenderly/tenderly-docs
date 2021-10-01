# ETH Balance

{% embed url="https://www.loom.com/share/81a9b4a9f49d4c6a887f2d01d3b850a6" %}

#### Introduction

Triggers when the ETH balance of an address falls below a certain threshold.

{% hint style="warning" %}
This alert is triggered only when a transaction reduces the balance of the address below the set threshold. It will not be triggered while it is below the set threshold.
{% endhint %}

#### Example

Let’s get notified when the contract balance falls below a set threshold.

* First of all, we need to add Smart Contract to Project. You can see here how to **\[Add new contract\]** into Project.

* Click on **Alerting** in the navigation **—&gt;** **New Alert** **—&gt;** **ETH Balance —&gt; Contract —&gt; Select Contract —&gt;**Find Smart Contract and Choose it **—&gt;** Enter threshold in Wei **—&gt; Next —&gt;** Choose Alert Destination **—&gt; Save.** 
* That’s it! You’ll get a notification whenever the contract balance falls below a set threshold. 
* When Alert was created if we want to add a description, alert level, more alert destinations, or change the name, we can do that. You can see how in [Edit Alert](editing-an-alert.md).

