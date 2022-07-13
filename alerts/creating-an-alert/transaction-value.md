# Transaction Value

![](<../../.gitbook/assets/Creating an Alert - Transaction Value.png>)

#### Introduction

This alert type triggers whenever a transaction value matches certain conditions.

#### Example

Let’s get notified for every transaction above 100 ETH that calls the selected contract.

* [Start by **adding a Smart Contract**](https://docs.tenderly.co/monitoring/smart-contracts) **** to a Project by choosing one of the available options.
* Click **Alerting** in the navigation **—>** **New Alert** **—>** **Transaction Value —> Contract —> Select Contract —>** Find the added Smart Contract **—>**Choose the contract **—>** Select the **`>`** comparator **—>** Enter **100000000000000000000** Wei **—> Next —>**Choose an Alert Destination **—> Save.**
* Once everything is set up, you'll receive notifications whenever a transaction with more than 100 Ether calls the specified contract.
* Rename your new alert, add a description, choose multiple destinations, or set an alert level by [going to the Edit Alert settings](https://docs.tenderly.co/alerts/creating-an-alert/editing-an-alert).&#x20;
