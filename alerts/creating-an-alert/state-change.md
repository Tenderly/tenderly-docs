# State Change

{% embed url="https://www.loom.com/share/a44855423ddb4f2c81796d0cad8ba670" %}

#### Introduction

Triggers whenever a state variable in one of your contracts changes.

#### Example

Let’s get notified when MultiSigWallet number of required confirmations go below 5.

* First of all, we need to add a MultiSigWallet Smart Contract to Project. You can see there how to **\[Add new contract\]** into Project.

* Click on **Alerting** in the navigation **—&gt;** **New Alert** **—&gt;** **State Change —&gt; Contract —&gt; Select Contract —&gt;**Find MultiSigWallet Smart Contract and Choose it **—&gt;** Select variable **`required`** **—&gt;** Click on **Criteria** **—&gt;** Select `**<**` **—&gt;** Enter comparison value **5 —&gt; Next —&gt;** Choose Alert Destination **—&gt; Save.** 
* That’s it! You’ll get a notification whenever the number of required confirmations go below 5. 
* When Alert was created if we want to add a description, alert level, more alert destinations, or change the name, we can do that. You can see how in [Edit Alert](editing-an-alert.md).

