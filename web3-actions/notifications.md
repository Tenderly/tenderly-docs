# Notifications

Since Web3 Actions can be used as a part of 'critical workflows' (aside from all the other uses) it would be extremely prudent to have notifications delivered outside Tenderly Dashboard (email for starters, other channels will be added soon) so you can react quickly if need be when a certain Web3 Action you set up fails to execute.

![](<../.gitbook/assets/Screenshot 2022-04-14 at 11.23.59.png>)

**You can now set up an email as a destination where you will receive Tenderly notifications about failed executions of your set Web3 Action(s)**, by clicking on any Action and scrolling down to the "Destinations" section:

![](<../.gitbook/assets/Screenshot 2022-04-14 at 11.32.16.png>)

![](<../.gitbook/assets/Screenshot 2022-04-14 at 11.36.52.png>)

We already have a couple of email destinations set up which we can turn on or off so we don't have to delete certain email delivery channels in periods when we don't want to use them.&#x20;

In order to add a new email delivery channel, just click on the `Add Destination Email` button in the bottom right, type in the email you want to use and that's it.&#x20;

You will need to verify your email though for obvious reasons, and turn the switch for that email to "on" after the verification. You can also choose multiple emails as delivery channels for a single Action. If you are adding the email you are already using as your account email, or if you added that email through some other flow to Tenderly (e.g. through Alerts), your email will be recognized and you won't have to verify it again.

![](<../.gitbook/assets/Screenshot 2022-04-14 at 11.48.25.png>)

You are also able to choose the email notification delivery channels when creating a new action, although if you want to add a new email as a destination you will have to do that first before choosing it as an option in the "Create New Action" flow.

![](<../.gitbook/assets/Screenshot 2022-04-14 at 11.59.48.png>)

You will not be spammed by email if your Actions fails - we will be grouping all of the errors for your Action and sending you notifications in 15 minute intervals, starting with the first error occurrence.
