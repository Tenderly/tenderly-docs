# Creating an Alert

{% embed url="https://vimeo.com/637795807" %}

{% hint style="warning" %}
First of all, before creating an alert we need to configure Alert destination. If you haven't done that yet [check out how to configure Alert destinations.](../alerting/alert-targets/configuring-alert-destinations.md)
{% endhint %}

### Get an alert when a transaction fails

Let’s say I want to get alerted whenever any of your Smart Contracts fail. What you would do is the following:

![](../../.gitbook/assets/1-cgb4lf9qcz\_h-ssu2-cqha.gif)

Now if a transaction ever fails, you get notified instantly. This means that you can act immediately instead of waiting for your Dapp users to tell you that something isn’t working, like in the following Alert example:

![](<../../.gitbook/assets/image (28).png>)

You can read more broadly about this on [https://blog.tenderly.co/how-to-set-up-real-time-alerting-for-smart-contracts-with-tenderly/](https://blog.tenderly.co/how-to-set-up-real-time-alerting-for-smart-contracts-with-tenderly/).

### Testing created alerts

You can run an alert test for any of the alerts you are creating or have already created, and you will see how that alert will behave.

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 13.49.32.png>)

It's as simple as clicking on `Trigger Test Alert` button in the bottom left of the screen:

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 13.51.52.png>)

You will be prompted to choose the network you want to test your alert on (depending if your contract/wallet is multi-network or not) and to paste the transaction hash you want to run the alert test for (you can see all the transactions for any account ):

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 13.52.55.png>)

If the alert test fails you will get the following notification about it:

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 14.10.02.png>)

If the alert test succeeds you will get a notification in the bottom right of your screen. You can go to your **Alert History in the Alerts Tab** and see all successful tests for your alert(s) - they are clearly marked so you don't confuse them with the instances where your alert was actually triggered.

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 14.17.24.png>)

You can also click on any of your alerts and easily **Duplicate** them **** by clicking on the button in the bottom right of the screen, right next to the **Edit** button:

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 14.18.09.png>)

If you don't want your alert to trigger for whatever reason, you can **Disable** it instead of deleting it, bi clicking on the button in the bottom left of the same screen:

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 14.21.21.png>)
