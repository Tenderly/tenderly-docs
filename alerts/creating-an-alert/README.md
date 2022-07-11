# Creating an Alert

{% embed url="https://vimeo.com/637795807" %}

{% hint style="warning" %}
First of all, before creating an alert, we need to configure a destination. If you haven't done that yet, [check out how to configure Alert destinations.](../alerting/alert-targets/configuring-alert-destinations.md)
{% endhint %}

### Get an alert when a transaction fails

To get alerted whenever any of your Smart Contracts fail, make sure to follow these steps:

![](<../../.gitbook/assets/Creating an Alert for a failed transaction.gif>)

Once you set this up, you'll get an instant notification if a transaction fails. This way, you can act immediately instead of waiting for your dApp users to tell you that something isn’t working. Take a look at the following Alert example:

![](<../../.gitbook/assets/image (28).png>)

For more information, learn [how to set up Alerts for Smart Contracts in real time](https://blog.tenderly.co/how-to-set-up-real-time-alerting-for-smart-contracts-with-tenderly/).

### Test the created alerts

You can run a test for any new or existing alert to see how it will behave.

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 13.49.32.png>)

It's as simple as clicking the `Trigger Test Alert` button in the bottom left corner:

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 13.51.52.png>)

Choose the network you want to test your alert on (depending on whether your contract/wallet is multi-network or not). Next, paste the transaction hash for which you want to run the alert test (you can see all the transactions for any account):

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 13.52.55.png>)

If the alert test fails, you'll get the following notification:

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 14.10.02.png>)

If the alert test is successful, you'll get a notification in the bottom right corner of your screen. Go to **Alert History in the Alerts tab** for an overview of all the successful tests for your alert(s). They are clearly marked so you don't confuse them with the instances where your alert was actually triggered.

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 14.17.24.png>)

You can also click any alert to easily **Duplicate** it. Simply click the button in the bottom right corner, right next to **Edit**:

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 14.18.09.png>)

If you don't want your alert to trigger for whatever reason, you can **Disable** it instead of deleting it. Just click the button in the bottom left corner of the same screen:

![](<../../.gitbook/assets/Screenshot 2022-03-15 at 14.21.21.png>)
