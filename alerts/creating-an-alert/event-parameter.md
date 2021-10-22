# Event Parameter

![](../../.gitbook/assets/Event-Parameter.gif)

#### Introduction

Triggers whenever a specific event argument in an event matches the set of conditions.

#### Example

Let’s get notified every time when a spender is granted rights to withdraw tokens from our address.

*   First of all, we need to add some ERC20 Smart Contract to Project. You can see here how to **\[Add new contract]** into Project.


* Click on **Alerting** in the navigation **—>** **New Alert** **—>** **Event Parameter —> Contract —> Select Contract —>**Find ERC20 Smart Contract and Choose it **—>** Choose **Approval** event **—>** Select **owner** argument **—>** Select comparator **equal to —>** Paste your address  **—> Next —>** Choose Alert Destination **—> Save.**\
  ****
* That’s it! You will be notified whenever an approval call is set for additional spending for our address.\

* When Alert was created if we want to add a description, alert level, more alert destinations, or change the name, we can do that. You can see how in [Edit Alert](editing-an-alert.md).
