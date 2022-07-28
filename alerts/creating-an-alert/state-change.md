# State Change

![](<../../.gitbook/assets/Creating an Alert - State Change 1.png>)

#### Introduction

Use this alert type to receive notifications whenever a state variable in one of your contracts changes.

#### Example

Here are a few steps to help you create an alert that will notify you when the number of required confirmations for a MultiSigWallet goes below 5.

* Choose one of the [ways to add a new contract to Projects](https://docs.tenderly.co/monitoring/smart-contracts) first and import your MultiSigWallet Smart Contract.
* Set up a new alert by going to the **Alerting** tab in the left side bar **—>** **New Alert** **—>** **State Change —> Address —> Select Address —>**Choose the MultiSigWallet Smart Contract **—>** Select the **`required`** variable **—>** Click **Criteria** **—>** Select `**<**` **—>** Enter **5** as the comparison value **—> Next —>** Choose an Alert Destination **—> Save.**
* Your alert will send you a notification whenever the number of required confirmations goes below 5.
* You can [edit your existing alert in a few ways](https://docs.tenderly.co/alerts/creating-an-alert/editing-an-alert). Customize it by changing the name, writing a description, choosing multiple destinations, or setting up an alert level.&#x20;
