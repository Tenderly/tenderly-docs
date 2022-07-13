# ETH Balance

![](<../../.gitbook/assets/Creating an Alert - ETH Balance.png>)

#### Introduction

This alert type notifies you when the ETH balance of an address falls below a certain threshold.

{% hint style="warning" %}
This alert is triggered only when a transaction reduces the balance of the address below the specified threshold. It won't be triggered while the balance is below the set threshold.
{% endhint %}

#### Example

Here's how you can create this type of alert and start receiving notifications when the contract balance falls below a certain threshold.

* The first step entails [adding a Smart Contract to your Project](https://docs.tenderly.co/monitoring/smart-contracts).
* Once you add the contract, go to **Alerting** in the side navigation **—>** **New Alert** **—>** **ETH Balance —> Contract —> Select Contract —>**Find & Choose the needed Smart Contract **—>** Enter a threshold in Wei **—> Next —>**Choose an Alert Destination **—> Save.**
* After implementing the previous steps, you’ll get a notification whenever the contract balance falls below the specified threshold.
* Explore different [ways to edit your newly created Alert](https://docs.tenderly.co/alerts/creating-an-alert/editing-an-alert). You can update its name, add a description, set up an alert level, or choose multiple destinations.
