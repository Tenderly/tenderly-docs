# Configuring Alert Destinations

Alert destinations need to be set up only once per organization, then it is available for all projects.

{% hint style="warning" %}
#### All destinations are shared account-wide on all projects. If you edit or delete a destination it will be applied to all projects and active rules.
{% endhint %}

Open Destinations tab:

![](<../../../.gitbook/assets/image (56).png>)

## Email

Go to **Alerting** -> **Destinations** and click on **Email** to add a new email for alert delivery:

![](<../../../.gitbook/assets/Screenshot 2021-10-15 at 10.59.46.png>)

You will get a verification request to your email, copy or click on the link to confirm verification and that's it, your alerting notification will now be delivered to this email as well.

## Slack

You can connect Tenderly with your Slack workspace and get real-time notifications when an alert rule matches a transaction. Connecting multiple channels is also supported so you can route certain rules to specific channels.

Navigate to a project and go to the **Alerts** tab.

![](../../../.gitbook/assets/preview.tenderly.dev\_project\_uber-cool-project\_alerts\_rules.png)

Click on **Destinations**.

![](<../../../.gitbook/assets/preview.tenderly.dev\_project\_uber-cool-project\_alerts\_destinations (1).png>)

Finally click on **Slack** and then **Connect Slack**.

![](<../../../.gitbook/assets/preview.tenderly.dev\_project\_uber-cool-project\_alerts\_destinations-1 (1).png>)

You will be greeted with the Slack permissions screen where you will pick to which channel you want your notification to get delivered.

![](../../../.gitbook/assets/screen-shot-2019-09-02-at-11.42.40.png)

And that's it! Now when a transaction matches a configured alert rule you will get a notification instantly delivered to your Slack channel.

![](../../../.gitbook/assets/screen-shot-2019-08-30-at-13.08.01.png)

{% hint style="info" %}
Check out how to [create an Alert here.](../../creating-an-alert/)
{% endhint %}

## Telegram

Go to **Alerting** -> **Destinations** and click on **Telegram** to add a new Telegram channel for alert delivery:

![](<../../../.gitbook/assets/Screenshot 2021-10-15 at 11.03.01.png>)

And just follow the onscreen instructions:

![](<../../../.gitbook/assets/Screenshot 2021-10-15 at 11.03.42.png>)

Discord

Go to **Alerting** -> **Destinations** and click on **Discord** to connect a Discord channel for alert delivery.&#x20;

Firstly you will need to open your Discord, go to **Settings** -> **Integrations** -> **New Webhook**, name it and choose a Discord delivery channel, and copy the Webhook URL back into Tenderly:

![](<../../../.gitbook/assets/Screenshot 2021-10-15 at 11.07.45.png>)

![](<../../../.gitbook/assets/Screenshot 2021-10-15 at 11.08.46.png>)

## Sentry

It is pretty straightforward when it comes to adding a new alert destination but let's go over it. On your Tenderly Dashboard go to **Alerting,** which can be found under **Monitoring**, choose the **Destinations** tab:

![](<../../../.gitbook/assets/image (43).png>)

* Now that you can see all the available Destinations pick **Sentry.**\
  ****
* A window will pop-up which will ask you for your DSN Address and a Label for you to choose ("You can find your project’s DSN in the “**Client Keys**” section of your “**Project Settings**” in Sentry").

![](<../../../.gitbook/assets/image (64).png>)

And voilà! Your Sentry project is now connected with Tenderly:

![](<../../../.gitbook/assets/image (41).png>)

## PagerDuty

All you have to do is go to the "**Destinations**" tab as you would do for Sentry, pick PagerDuty and click on "**Connect PagerDuty**":

![](<../../../.gitbook/assets/image (29).png>)

You will get redirected to PagerDuty's page, where you can approve Tenderly as a source.

![](<../../../.gitbook/assets/image (36).png>)

If done correctly, PagerDuty should be under your **Active Destinations.**

## **Web3 Actions**

An alert trigger means your action will be used as a [**destination for the alert**](../../creating-an-alert/).

```yaml
trigger:
  type: alert
  alert: {}
```

A single action can be used as a destination for multiple alerts.

&#x20;**** [You can read more about this and Web3 Actions in general here.](../../../web3-actions/triggers.md)
