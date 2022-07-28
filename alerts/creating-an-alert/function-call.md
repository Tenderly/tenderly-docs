# Function Call

![](<../../.gitbook/assets/Creating an Alert - Function Call 1.png>)

#### Introduction

This type of alert triggers whenever a specific function is called in one of your Smart Contracts. By setting up this alert, you can receive a notification not only when a function is first called in a transaction, but each time it's called during the execution of a transaction.

#### Example

Let’s set up an Alert to notify us every time a new CryptoKitty is born by following these steps:&#x20;

* Add the CryptoKitties contract to Projects. _The_ _CryptoKitties Smart Contract address is 0x06012c8cf97bead5deae237070f9587f8e7a266d_. Follow a few [steps to **Add a new contract** to your Projects](https://docs.tenderly.co/monitoring/smart-contracts).&#x20;
* Click **Alerting** in the side navigation menu **—>** **New Alert** **—>** **Function Call —> Contract —> Select Contract —>**Find and Choose the **KittyCore** Smart Contract **—>** Choose the **giveBirth** function **—> Next —>**Choose Alert Destination **—> Save.**
* You’ll receive a notification whenever a CryptoKitty comes into the Ethereum world.
* ****[**Edit your new Alert**](https://docs.tenderly.co/alerts/creating-an-alert/editing-an-alert) by filling in a description, adding an alert level, setting more destinations, or changing its name.&#x20;

![](<../../.gitbook/assets/Creating an Alert - Function Call 2.png>)
