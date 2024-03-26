---
description: Learn how to create your first webhook and start receiving alerting events.
---

# How to Use Webhooks for Alerting

Welcome to this guide on how to create a webhook as an alert destination to receive events from an alerting service. In this guide, you will learn how to set up a webhook and see its execution.

### Adding a webhook as an alert destination

{% hint style="info" %}
To continue, [log into your account](https://dashboard.tenderly.co/) or [create a free account](https://dashboard.tenderly.co/register) if you don’t have one.
{% endhint %}

Once logged in, create a new [Tenderly project](https://docs.tenderly.co/projects) or select an existing one where you want to create your Webhook.

From the left-hand menu, go to **Alerts ->** **Destinations** tab, where you'll see a list of [all the available destinations](../configuring-alert-destinations/).

<figure><img src="../../.gitbook/assets/image (56).png" alt=""><figcaption><p>Navigating to the Destination section</p></figcaption></figure>

To create a webhook alert destination, click on the Webhook card, which will open up the configuration modal. You'll be prompted to configure the following options:&#x20;

* **Webhook name** - Must be unique and cannot be changed later
* **Webhook URL** - URL where you'll receive live events from Tenderly
* **Description** - Optional parameter, but you can use it to provide more information about the webhook configuration

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption><p>Add Webhook Modal</p></figcaption></figure>

If you click on the **Advanced Configuration** link, a modal will open with JavaScript, Python, or Go code snippets that you can use to set up your custom webhook.

<figure><img src="../../.gitbook/assets/image (100).png" alt=""><figcaption><p>Webhook Modal Advanced Configuration Modal</p></figcaption></figure>

To test if the provided URL is able to receive events from Tenderly, click on the **Send test webhook** button, and the predefined test payload will be sent to your endpoint.

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption><p>Send Test Webhook</p></figcaption></figure>

If everything works as expected and you've received the event, click on the **Add Webhook** button. This action will add the new webhook destination to the **Active Destinations** list.

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption><p>New Webhook is added to the active destinations list</p></figcaption></figure>

Clicking on the button to the right will open up the Webhook overview page. This is where you can find information about the webhook status, URL, creation date, signing secrets, etc.

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption><p>Webhook Page</p></figcaption></figure>

You also perform other actions on your webhooks, such as enabling/disabling a webhook, or make changes to the existing configuration.&#x20;

**Enable/Disable Webhook:**  Toggle the status of a webhook between active and inactive.&#x20;

**Delete Webhook**: Remove a webhook from your Tenderly project. Deleting a webhook is a permanent action and cannot be undone.

<figure><img src="../../.gitbook/assets/image (101).png" alt=""><figcaption><p>Webhook Options</p></figcaption></figure>

**Send a Test Request:** Test the functionality of your webhook by sending a test event to the provided URL by providing a transaction hash with its network.

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption><p>Test Webhook Modal</p></figcaption></figure>

**Edit Webhook**: Modify the configuration of an existing webhook, such as the URL or description.

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption><p>Edit Webhook Modal</p></figcaption></figure>

### Webhook execution history

From the webhook overview page, click on Execution History to see the transaction payload that has been sent to the provided webhook URL and the response from the webhook endpoint.

<figure><img src="../../.gitbook/assets/image (1) (3) (1).png" alt=""><figcaption><p>Manually Triggered Webhook After Clicking on Test Webhook Button</p></figcaption></figure>

Webhook execution can have several statuses:

* **Success:** Webhook was successfully executed, and the event was delivered to the specified URL.
* **Failed**: Webhook was unable to be executed due to an error, such as a connectivity issue, a problem with the URL, or something else. Check the response content to see what caused the error, or contact our support.
* **Pending**: Webhook is in the process of being executed and has not yet been completed.
* **Retry**: Webhook execution failed but will be retried no more than 5 times until it changes the status to Success or Failed.
* **Skipped**: Webhook was not executed because it was disabled.

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>Webhook Execution Page</p></figcaption></figure>

You can also see prior webhook executions by applying different filters, such as **Filter by Status** and **Select a Date Range**.

<figure><img src="../../.gitbook/assets/image (13) (2).png" alt=""><figcaption><p>Webhook Execution History Page</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption><p>Select Webhook Status Dropdown</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>Select Date Range Dropdown</p></figcaption></figure>

### Connecting a webhook to an Alert

With your webhook endpoint configured, you can add it as a Destination to any of your Alerts.

{% hint style="success" %}
[Follow this guide](alerting-quickstart-guide.md) to learn how to set up an Alert.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (2) (2).png" alt=""><figcaption><p>Adding a Webhook as a Destination to the Alert Rule</p></figcaption></figure>

When you create an Alert rule, you'll be redirected to the following page:

<figure><img src="../../.gitbook/assets/image (8) (2).png" alt=""><figcaption><p>Alert Rule with a Webhook as a Destination</p></figcaption></figure>

If your Alert is enabled, you'll start receiving events to your webhook endpoint.&#x20;

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption><p>Webhook Execution History Page</p></figcaption></figure>

In this example, we used [https://webhook.site](https://webhook.site/) to create a temporary webhook endpoint to test how Tenderly webhooks work. Below is an image of the payload successfully sent to the webhook.

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>Successful Webhook Executions</p></figcaption></figure>
