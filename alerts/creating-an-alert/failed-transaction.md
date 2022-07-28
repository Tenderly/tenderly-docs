# Failed Transaction

![](<../../.gitbook/assets/Creating an Alert for a failed transaction.gif>)

#### Introduction

Trigger your Alert whenever a transaction that calls your Smart Contracts fails. You can set up different targets, such as when a transaction calls a contract or, a more general one, when a transaction is created on a particular network.

#### Example 1

Let’s say we deployed a Smart Contracts and want to monitor every failed transaction that calls it. To do this, we need to implement the following:&#x20;

* First of all, we need to add the contract to Projects. [**Adding a new contract** to a Project ](https://docs.tenderly.co/monitoring/smart-contracts)requires just a few steps.&#x20;
* Click **Alerting** in the navigation **—>** **New Alert** **—>** **Failed Transaction —> Contract —> Select Contract —>** Find and select the Contract you want to monitor **—> Next —>** Choose Alert Destination **—> Save.**
* That's it! We've set up a new Alert that will instantly notify us if a transaction calling our contract fails.
* We can also [edit the Alert](https://docs.tenderly.co/alerts/creating-an-alert/editing-an-alert) to change its name and add a description, alert level, and more destinations.

#### Example 2

In this example, we created an Alert that will notify us whenever a transaction fails on the DAI Smart Contract. After setting up the Alert, we need to choose a destination:

![](<../../.gitbook/assets/image (66).png>)

Here, we’ll select Sentry and PagerDuty as destinations.

After setting this up, whenever a DAI transaction fails, you'll receive a detailed Alert via Sentry and PagerDuty.

As you can see, the whole error stack trace can be found in your Sentry dashboard:

![](<../../.gitbook/assets/image (48).png>)

PagerDuty gives you a more straightforward insight into the issue:

![](<../../.gitbook/assets/image (58).png>)

![](<../../.gitbook/assets/image (8).png>)
