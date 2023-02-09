---
description: >-
  This page walks you through how to create each account-scoped Alert
  Destination.
---

# Account-Scoped

Account-scoped Destinations are accessible across all your projects within your Tenderly account.

### Email Destination

<figure><img src="../../.gitbook/assets/email_dest.png" alt=""><figcaption><p>Email destination configurations</p></figcaption></figure>

Get an Alert notification in your email inbox.

Go to **Alerts →** **Destinations → Email.**

**Click Add Email.**

A verification email will be sent to the email address you provided. Click the link in the email to confirm that you’re the owner of the email address.

### Slack Destination

<figure><img src="../../.gitbook/assets/slack_dest.png" alt=""><figcaption><p>Slack destination configurations</p></figcaption></figure>

Get Alert notifications in a private message or a channel on Slack.

Go to **Alerts →** **Destinations → Slack → Connect Slack.**

This will take you to the Slack permissions screen, where you need to set the Slack channel or private message to receive notifications.

### Telegram Destination

<figure><img src="../../.gitbook/assets/telegram_dest.png" alt=""><figcaption><p>Telegram destination configurations</p></figcaption></figure>

Get Alert notifications in a Telegram channel.

Go to **Alerts →** **Destinations → Telegram.**

Add a required label for the Telegram Destination and click Next.

**Follow the instruction** on the screen to connect to TenderlyRobot for Telegram and **click Finish**.

### Discord Destination

<figure><img src="../../.gitbook/assets/slack_dest_(1).png" alt=""><figcaption><p>Discord destination configurations</p></figcaption></figure>

Get Alert notifications in a Discord channel.

Go to **Alerts →** **Destinations → Discord.**

Add a required label and paste your Discord webhook. Follow this [official guide from Discord](https://support.discord.com/hc/en-us/articles/228383668-Intro-to-Webhooks) to get the webhook URL.

**Click Add Webhook**.

### Sentry Destination

<figure><img src="../../.gitbook/assets/sentry_dest.png" alt=""><figcaption><p>Sentry destination configurations</p></figcaption></figure>

Send Alert data to Sentry, a third-party application alert monitoring and error tracking platform.

Go to **Alerts →** **Destinations → Sentry.**

Add a required label and paste the Sentry DSN key. Check the [official Sentry documentation](https://docs.sentry.io/product/sentry-basics/dsn-explainer/) to learn how to find your project DSN.

**Click Connect Sentry**.

### PagerDuty Destination

<figure><img src="../../.gitbook/assets/pageryduty_dest.png" alt=""><figcaption><p>PagerDuty destination configurations</p></figcaption></figure>

Send Alert data to PageryDuty, a third-party incident response platform.

Go to **Alerts →** **Destinations → PagerDury → Connect PagerDuty.**

You'll get redirected to a PagerDuty page and asked to add the Tenderly PagerDuty App to your workspace and authorize a specific channel to receive Alert notifications.
