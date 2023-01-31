---
description: Learn how to create your first webhook and start receiving alerting events
---

# How to Use Webhooks for Alerting

Welcome to this guide on creating a webhook to receive events from an alerting service. In this guide, you will learn how to set up a webhook and see its execution.

### Adding a Webhook as an alert destination

{% hint style="info" %}
To continue, [log into your account](https://dashboard.tenderly.co/) or [create a free account](https://dashboard.tenderly.co/register) if you don’t have one.
{% endhint %}

Once logged in, create a new [Tenderly project](https://docs.tenderly.co/projects) or select an existing one where you want to create your Webhook.

From the left-hand menu, select **Alerts**, and navigate to the **Destinations** tab.

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption><p>Navigating to the Destination section</p></figcaption></figure>

You will be provided with the list of all destinations.

In order to create your first webhook, you can click on the Webhook card and the configuration modal will pop up. You'll have an option to set the:

* **Webhook name** - it must be unique and cannot be changed later
* **Webhook URL** - an URL where you'll receive live events from Tenderly
* **Description** - this is an optional parameter, but it can be used to provide more information about the webhook configuration

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption><p>Add Webhook Modal</p></figcaption></figure>

If you click on the advanced configuration link, a modal will open with code snippets in JavaScript, Python, or Go that you can use to set up your webhook more easily.

<figure><img src="../../.gitbook/assets/image (100).png" alt=""><figcaption><p>Webhook Modal Advanced Configuration Modal</p></figcaption></figure>

If you'd like to test if the provided URL is able to receive events from Tenderly, you can click on the **Send test webhook** button and the a predefined test payload will be sent to your endpoint.

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption><p>Send Test Webhook</p></figcaption></figure>

If everything works well and you've received an event, you can click on the **Add Webhook** button and the **Active Destinations** list will be updated.

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption><p>New Webhook is added to the active destinations list</p></figcaption></figure>

You can click the button on the right in order to open the Webhook page. The page will provide webhook info such as status, URL, when it is created, ability to sign key, etc.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption><p>Webhook Page</p></figcaption></figure>

A single webhook provides many more actionable options than other destinations. You can:

* Enable/Disable Webhook - It allows you to toggle the status of a webhook between active and inactive. This can be useful if you want to temporarily stop receiving events from Tenderly.
* Send a Test Request - It allows you to test the functionality of your webhook by sending a test event to the provided URL by providing a transaction hash with its network. This can be helpful to ensure that your webhook is correctly configured and working as intended.
* Edit Webhook - It allows you to modify the configuration of an existing webhook, such as the URL, or description. This can be useful if you need to update the webhook to reflect changes in your Tenderly project.
* Delete Webhook - It allows you to permanently remove a webhook from your Tenderly project. This can be useful if you no longer need the webhook or if you want to free up resources by deleting unnecessary webhooks. Please note that deleting a webhook is a permanent action and cannot be undone.

<figure><img src="../../.gitbook/assets/image (101).png" alt=""><figcaption><p>Webhook Options</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption><p>Disable Webhook Modal</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption><p>Enable Webhook Modal</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption><p>Test Webhook Modal</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Edit Webhook Modal</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Manually Triggered Webhook After Clicking on Test Webhook Button</p></figcaption></figure>

You can click on the webhook execution item from the list and go to the Webhook Execution page. This page is useful because you can see the transaction payload that has been sent to the provided webhook URL and the response from the webhook endpoint.

{% hint style="info" %}
Webhook execution can have several statuses:

* **Success** - indicates that the webhook was successfully executed and the event was delivered to the specified URL
* **Failed** - indicates that the webhook was unable to be executed due to an error, such as a connectivity issue, a problem with the URL, or something else (check the response content to see what caused the error or contact our support)
* **Pending** - indicates that the webhook is in the process of being executed and has not yet been completed
* **Retry** - indicates that the webhook execution failed but will be retried no more than 5 times until it changes the status to Sucess or Failed
* **Skipped** - indicates that the webhook was not executed because it was disabled
{% endhint %}

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Webhook Execution Page</p></figcaption></figure>

### Webhook Execution History

To see all webhook executions, you can click on the **Execution History** tab. This page provides several filters such as **Filter by Status** and **Select a Date Range**.

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption><p>Webhook Execution History Page</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption><p>Select Webhook Status Dropdown</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>Select Date Range Dropdown</p></figcaption></figure>

### Connecting a Webhook to Alert

Finally, when you have finished setting up your webhook endpoint, you can add it as a destination to any of your alert rules.

{% hint style="info" %}
In order to see how to create an Alert Rule, you can follow [these instructions](https://docs.tenderly.co/alerts/creating-an-alert).
{% endhint %}

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Adding a Webhook as a Destination to the Alert Rule</p></figcaption></figure>

When you create an alert rule, you'll be redirected to the following page:

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption><p>Alert Rule with a Webhook as a Destination</p></figcaption></figure>

If your alert is enabled, you'll start receiving events to your webhook endpoint. You can go to the **Webhook Execution History** page to see all executions.

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption><p>Webhook Execution History Page</p></figcaption></figure>

In this example, we used [https://webhook.site](https://webhook.site/) to create a Webhook Endpoint in order to test out how Tenderly Webhooks work. Below is an image of the successfully sent transaction payloads.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Successful Webhook Executions</p></figcaption></figure>
