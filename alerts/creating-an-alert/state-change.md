# State Change

![](<../../.gitbook/assets/State Change.gif>)

#### Introduction

Triggers whenever a state variable in one of your contracts changes.

#### Example

Let’s get notified when MultiSigWallet number of required confirmations go below 5.

*   First of all, we need to add a MultiSigWallet Smart Contract to Project. You can see there how to **\[Add new contract]** into Project.


* Click on **Alerting** in the navigation **—>** **New Alert** **—>** **State Change —> Contract —> Select Contract —>**Find MultiSigWallet Smart Contract and Choose it **—>** Select variable **`required`** **—>** Click on **Criteria** **—>** Select `**<**` **—>** Enter comparison value **5 —> Next —>** Choose Alert Destination **—> Save.**\
  ****
* That’s it! You’ll get a notification whenever the number of required confirmations go below 5.\

* When Alert was created if we want to add a description, alert level, more alert destinations, or change the name, we can do that. You can see how in [Edit Alert](editing-an-alert.md).
