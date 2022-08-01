# Event Parameter

![](<../../.gitbook/assets/Creating an Alert - Event Parameter.png>)

#### Introduction

This alert type triggers whenever a specific event argument in an event matches a set of conditions.

#### Example

You can receive a notification every time a spender is granted rights to withdraw tokens from your address by following these steps:&#x20;

* First you need to add an ERC20 Smart Contract to Projects. There are several ways to [Add a new contract to a Project](https://docs.tenderly.co/monitoring/smart-contracts).
* Go to **Alerting** in the left side bar **—>** **New Alert** **—>** **Event Parameter —> Address —> Select Address —>**Find the ERC20 Smart Contract **—>** Choose the **Approval** event **—>** Select the **owner** argument **—>** Select the **equal to** comparator **—>**Paste your address  **—> Next —>** Choose an Alert Destination **—> Save.**
* You'll be notified whenever an approval call is set for additional spending for your address.
* After creating an Alert, you can add a description, alert level, more alert destinations, or a new name. You're able to do this by [editing your existing Alert](https://docs.tenderly.co/alerts/creating-an-alert/editing-an-alert).
