# Transaction Value

![](../../.gitbook/assets/Transaction-Value.gif)

#### Introduction

Triggers whenever a transaction value matches set conditions.

#### Example

Let’s get notified for every transaction above 100 Ether who called the selected contract.

*   First of all, we need to add Smart Contract to Project. You can see here how to **\[Add new contract]** into Project.


* Click on **Alerting** in the navigation **—>** **New Alert** **—>** **Transaction Value —> Contract —> Select Contract —>** Find Smart Contract and Choose it **—>** Select comparator **`>`** **—>** Enter **100000000000000000000** Wei **—> Next —>** Choose Alert Destination **—> Save.**\
  ****
* That’s it! You’ll get a notification whenever the transaction with more than 100 Ether is called a selected contract.\

* When Alert was created if we want to add a description, alert level, more alert destinations, or change the name, we can do that. You can see how in [Edit Alert](editing-an-alert.md).
