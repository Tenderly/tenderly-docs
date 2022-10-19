---
description: >-
  Learn how to set up notifications about failed Web3 Actions so you can react
  accordingly. Follow a step-by-step guide to add an email destination for your
  notifications.
---

# Notifications

Since Web3 Actions can be used as a part of 'critical workflows' (aside from all the other uses) it would be extremely prudent to have notifications delivered outside Tenderly Dashboard (email for starters, other channels will be added soon). Setting up notifications will allow you to react quickly if need be when a certain Web3 Action you set up fails to execute.

<figure><img src="../../.gitbook/assets/Screenshot 2022-04-14 at 11.23.59.png" alt="Overview of the existing Web3 Actions "><figcaption><p>Overview of the existing Web3 Actions </p></figcaption></figure>

You can now set up an email as a destination where you will receive Tenderly notifications about failed executions of your set Web3 Action(s) by clicking any Action:&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2022-04-14 at 11.32.16.png" alt="Information about a specific Web3 Action"><figcaption><p>Information about a specific Web3 Action </p></figcaption></figure>

Scroll down to the Destinations section:

<figure><img src="../../.gitbook/assets/Screenshot 2022-04-14 at 11.36.52.png" alt="Choosing an email destination for Web3 Action notifications"><figcaption><p>Choosing an email destination for Web3 Action notifications</p></figcaption></figure>

We already have a couple of email destinations set up. We can turn them on or off so we don't have to delete certain email delivery channels in periods when we don't want to use them.&#x20;

To add a new email delivery channel, just click the **Add Destination Email** button in the bottom right corner, type in the email you want to use, and that's it.&#x20;

You will need to verify your email and turn the switch for that email to "on" after the verification. You can also choose multiple emails as delivery channels for a single Action.&#x20;

If you are adding an email you are already using as your account email, or if you added that email through some other flow to Tenderly (e.g. through Alerts), your email will be recognized and you won't have to verify it again.

<figure><img src="../../.gitbook/assets/Screenshot 2022-04-14 at 11.48.25.png" alt="Adding a new email address"><figcaption><p>Adding a new email address</p></figcaption></figure>

You are also able to choose the email notification delivery channels when creating a new action. However, if you want to add a new email as a destination, you will have to do that first before choosing it as an option in the Create New Action flow.

<figure><img src="../../.gitbook/assets/Screenshot 2022-04-14 at 11.59.48.png" alt="Choosing an email destination upon creating a Web3 Action "><figcaption><p>Choosing an email destination upon creating a Web3 Action </p></figcaption></figure>

You will not be spammed by email if your Actions fails. We group all of the errors for your Action and send you notifications at 15-minute intervals, starting with the first error occurrence.
