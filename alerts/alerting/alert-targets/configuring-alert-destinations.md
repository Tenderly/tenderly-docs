# Configuring Alert Destinations

Alert destinations need to be set up only once per organization and will be available for all projects.

{% hint style="warning" %}
#### All destinations are shared account-wide on all projects. If you edit or delete a destination, it will be applied to all projects and active rules.
{% endhint %}

Open Destinations tab:

![](<../../../.gitbook/assets/Configuring Alert Destinations.png>)

## Email

Go to **Alerting** -> **Destinations** and click **Email** to add a new email for alert delivery:

![](<../../../.gitbook/assets/Configuring Alert Destinations - Email.png>)

You'll get a verification request to your email. Copy or click the link to confim the verification and you'll receive alerting notifications via email as well.

## Slack

You can connect Tenderly to your Slack workspace and get real-time notifications when an alert rule matches a transaction. Connecting multiple channels is also supported, so you can route certain rules to specific channels.

Navigate to a project and go to the **Alerts** tab. Next, click **Destinations**.

![](<../../../.gitbook/assets/preview.tenderly.dev\_project\_uber-cool-project\_alerts\_destinations (1).png>)

Finally, click **Slack** and then **Connect Slack**.

![](<../../../.gitbook/assets/Configuring Alert Destinations - Slack.png>)

This will take you to the Slack permissions screen where you need to pick to which channel you want to receive your notifications.

![](../../../.gitbook/assets/screen-shot-2019-09-02-at-11.42.40.png)

And that's it! When a transaction matches a configured alert rule, you'll get a notification instantly delivered to your Slack channel.

![](../../../.gitbook/assets/screen-shot-2019-08-30-at-13.08.01.png)

{% hint style="info" %}
Check out how to [create an Alert here.](../../creating-an-alert/)
{% endhint %}

## Telegram

Go to **Alerting** -> **Destinations** and click **Telegram** to add a new Telegram channel for alert delivery:

![](<../../../.gitbook/assets/Configuring Alert Destinations - Telegram 1.png>)

Next, follow the onscreen instructions:

![](<../../../.gitbook/assets/Configuring Alert Destinations - Telegram  2.png>)

![](<../../../.gitbook/assets/Configuring Alert Destinations - Telegram 3.png>)

![](<../../../.gitbook/assets/Configuring Alert Destinations - Telegram 4.png>)

## Discord

Go to **Alerting** -> **Destinations** and click on **Discord** to connect a Discord channel for alert delivery.&#x20;

Firstly you will need to open your Discord, go to **Settings** -> **Integrations** -> **New Webhook**, name it and choose a Discord delivery channel, and copy the Webhook URL back into Tenderly:

![](<../../../.gitbook/assets/Screenshot 2021-10-15 at 11.07.45.png>)

![](<../../../.gitbook/assets/Screenshot 2021-10-15 at 11.08.46.png>)

## Sentry

Adding Sentry as a new alert destination is also pretty straightforward. In your Tenderly Dashboard, go to **Alerting** in the **Monitoring** section and choose the **Destinations** tab:

![](<../../../.gitbook/assets/image (43).png>)

Pick **Sentry** from the list of available Destinations. Next, a window will pop up asking you to fill in your DSN Address and a Label for you to choose. You can find your project DSN in the “**Client Keys**” section of your “**Project Settings**” in Sentry.

![](<../../../.gitbook/assets/Configuring Alert Destinations - Sentry.png>)

And voilà! Your Sentry project is now connected to Tenderly:

![](<../../../.gitbook/assets/image (41).png>)

## PagerDuty

Go to the **Destinations** tab, pick PagerDuty, and click **Connect PagerDuty**:

![](<../../../.gitbook/assets/Configuring Alert Destinations - PagerDuty.png>)

You'll get redirected to a PagerDuty page, where you can approve Tenderly as a source.

![](<../../../.gitbook/assets/image (36).png>)

If done correctly, PagerDuty should be under your **Active Destinations.**

## **Web3 Actions**

This type of alert trigger means your action will be used as a [**destination for the alert**](../../creating-an-alert/).

```yaml
trigger:
  type: alert
  alert: {}
```

A single action can be used as a destination for multiple alerts.

For more information, [read more about this and Web3 Actions in general](../../../web3-actions/intro-to-web3-actions/triggers.md).
