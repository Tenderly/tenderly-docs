# Alert Destinations

Tenderly sends alerts to Alerts Destinations. These include:

* Email
* Slack
* Telegram
* Discord
* Sentry
* PagerDuty
* Web3 Action
* Webhook

{% hint style="warning" %}
You can use a single destination for several different alerts. A destination target can be account-scoped or project-scoped.

**Account-scoped destinations:** Email, Slack, Telegram, Discord, Sentry, PagerDuty destinations are available for in projects.

**Project-scoped destinations:** Web3 Actions and Webhooks are are scoped to the project they're created in.



#### If you edit or delete a destination, it will be applied to all projects and active rules.
{% endhint %}

Open Destinations tab:

![](<../.gitbook/assets/Configuring Alert Destinations.png>)

## Email

Go to **Alerting** -> **Destinations** and click **Email** to add a new email for alert delivery:

![](<../.gitbook/assets/Configuring Alert Destinations - Email.png>)

You'll get a verification request to your email. Copy or click the link to confim the verification and you'll receive alerting notifications via email as well.

## Slack

You can connect Tenderly to your Slack workspace and get real-time notifications when an alert rule matches a transaction. Connecting multiple channels is also supported, so you can route certain rules to specific channels.

Navigate to a project and go to the **Alerts** tab. Next, click **Destinations**.

![](<../.gitbook/assets/preview.tenderly.dev\_project\_uber-cool-project\_alerts\_destinations (1).png>)

Finally, click **Slack** and then **Connect Slack**.

![](<../.gitbook/assets/Configuring Alert Destinations - Slack.png>)

This will take you to the Slack permissions screen where you need to pick to which channel you want to receive your notifications.

![](../.gitbook/assets/screen-shot-2019-09-02-at-11.42.40.png)

And that's it! When a transaction matches a configured alert rule, you'll get a notification instantly delivered to your Slack channel.

![](../.gitbook/assets/screen-shot-2019-08-30-at-13.08.01.png)

{% hint style="info" %}
Check out how to [create an Alert here.](creating-an-alert/)
{% endhint %}

## Telegram

Go to **Alerting** -> **Destinations** and click **Telegram** to add a new Telegram channel for alert delivery:

![](<../.gitbook/assets/Configuring Alert Destinations - Telegram 1.png>)

Next, follow the onscreen instructions:

![](<../.gitbook/assets/Configuring Alert Destinations - Telegram  2.png>)

![](<../.gitbook/assets/Configuring Alert Destinations - Telegram 3.png>)

![](<../.gitbook/assets/Configuring Alert Destinations - Telegram 4.png>)

## Discord

Go to **Alerting** -> **Destinations** and click on **Discord** to connect a Discord channel for alert delivery.&#x20;

Firstly you will need to open your Discord, go to **Settings** -> **Integrations** -> **New Webhook**, name it and choose a Discord delivery channel, and copy the Webhook URL back into Tenderly:

![](<../.gitbook/assets/Screenshot 2021-10-15 at 11.07.33.png>)

![](<../.gitbook/assets/Screenshot 2021-10-15 at 11.08.46.png>)

## Sentry

Adding Sentry as a new alert destination is also pretty straightforward. In your Tenderly Dashboard, go to **Alerting** in the **Monitoring** section and choose the **Destinations** tab:

![](<../.gitbook/assets/image (43).png>)

Pick **Sentry** from the list of available Destinations. Next, a window will pop up asking you to fill in your DSN Address and a Label for you to choose. You can find your project DSN in the “**Client Keys**” section of your “**Project Settings**” in Sentry.

![](<../.gitbook/assets/Configuring Alert Destinations - Sentry.png>)

And voilà! Your Sentry project is now connected to Tenderly:

![](<../.gitbook/assets/image (41).png>)

## PagerDuty

Go to the **Destinations** tab, pick PagerDuty, and click **Connect PagerDuty**:

![](<../.gitbook/assets/Configuring Alert Destinations - PagerDuty.png>)

You'll get redirected to a PagerDuty page, where you can approve Tenderly as a source.

![](<../.gitbook/assets/image (36).png>)

If done correctly, PagerDuty should be under your **Active Destinations.**

## **Web3 Actions**

This type of alert destination means your action will be used as a [**destination for the alert**](creating-an-alert/).

```yaml
trigger:
  type: alert
  alert: {}
```

A single action can be used as a destination for multiple alerts.

For more information, [read more about this and Web3 Actions in general](../web3-actions/intro-to-web3-actions.md).

## Webhooks

This alert destination allows for execution of your webhook when an alert is triggered. Your webhook will receive a signed payload, containing the transaction object that triggered the alert.&#x20;

{% hint style="info" %}
After adding a Webhook as an alert destination, you can use it as destination for other alerts.
{% endhint %}

{% content-ref url="how-to-use-webhooks-for-alerting.md" %}
[how-to-use-webhooks-for-alerting.md](how-to-use-webhooks-for-alerting.md)
{% endcontent-ref %}

#### The webhook requirements:

* It **must** expose a **GET** method with the webhook URI, that immediately returns `HTTP 200`. Tenderly makes a request to this method to verify the webhook is reachable.
* It **must** expose a **POST** method with the same webhook URI. The webhook will receive a payload described below.&#x20;
* Unless a `HTTP 200` doesn't respond within **5 seconds**, Tenderly considers this as a failed webhook execution.
* The webhook URL must use HTTPS.

{% hint style="warning" %}
The Webhook must respond within **5 seconds** time-frame. If there's no response, the execution is considered failed.&#x20;
{% endhint %}

Tenderly keeps track of all executions. Webhook execution can have several statuses:

* **Success** - indicates that the webhook was successfully executed and the event was delivered to the specified URL
* **Failed** - indicates that the webhook was unable to be executed due to an error, such as a connectivity issue, a problem with the URL, or something else (check the response content to see what caused the error or contact our support)
* **Pending** - indicates that the webhook is in the process of being executed and has not yet been completed
* **Retry** - indicates that the webhook execution failed but will be retried no more than 5 times until it changes the status to Sucess or Failed
* **Skipped** - indicates that the webhook was not executed because it was disabled

#### Webhook payload

The webhook will receive the payload representing the alerting event. The payload consists of three fields:

* **id**: `String` - ID unique accross all delivered alert events (UUID).
* **event\_type**: `TEST` | `ALERT` - the type of webhook event type.
* **transaction**: `Object` - an object representing an un-decoded transaction that triggered the alert and the webhook execution.&#x20;

Upon adding the webhook as an alert destination, it will be invoked with a `TEST` alert event type.&#x20;

{% hint style="info" %}
Use the `id` field to ensure your webhook processes each alert event exactly once, by keeping track of processed IDs.
{% endhint %}

#### Securing the Webhook

You can enhance security of your webhooks using the signature validation method. This way, you can verify that the request to webhook originates from Tenderly, before proceeding with the execution.

The  `x-tenderly-signature` header contains a cryptographic signature. The webhook request signature is a HMAC SHA256 hash of concatenated signing secret, request payload, and timestamp, in this order.

{% hint style="warning" %}
The Signing Secret is unique for each webhook destination. Tenderly generates this secret and uses it to generat a sigunature for the payload. Keep it at a safe place.
{% endhint %}

**Step 1.** Obtain the Secret Signing Secret.&#x20;

<figure><img src="../.gitbook/assets/image (49).png" alt=""><figcaption><p>Copying secret signing key</p></figcaption></figure>

**Step 2.** Validate the received signature

To validate the received signature, concatenate, in this order:

1. the signing secret,
2. the entire webhook request payload,
3. the timestamp (of the payload).

Lastly, perform a SHA 256 hash on the concatenated value.

{% tabs %}
{% tab title="Go" %}
```go
func isValidSignature(
	signature string,
	payload []byte,
	timestamp string,
) bool {
	h := hmac.New(sha256.New, []byte(signingKey))
	h.Write(payload)
	h.Write([]byte(timestamp))
	digest := hex.EncodeToString(h.Sum(nil))
	return digest == signature
}
```
{% endtab %}

{% tab title="JavaScript" %}
```javascript
function isValidSignature(signature, payload, timestamp) {
  // Create a HMAC SHA256 hash using the signing key
  const hmac = crypto.createHmac("sha256", signingKey); 
  
  // Update the hash with the request body using utf8
  hmac.update(payload.toString(), 'utf8'); 
  
  // Update the hash with the request timestamp
  hmac.update(timestamp);
  const digest = hmac.digest("hex");
  return crypto.timingSafeEqual(Buffer.from(signature), Buffer.from(digest))
}
```
{% endtab %}

{% tab title="Python" %}
```python
def isValidSignature(signature: string, payload: bytes, timestamp: string):
    h = hmac.new(str.encode(signingKey), payload, hashlib.sha256)
    h.update(str.encode(timestamp))
    digest = h.hexdigest()
    return hmac.compare_digest(signature, digest)
```
{% endtab %}
{% endtabs %}

#### Debugging Webhook executions

To support debugging of webhook malfunctions, you can manually send `TEST` events, based on existing transactions from any network

**Step 1.** Click "**Test Webhook**" in the navigation bar of the webhooks page.

<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption><p>Webhook overview</p></figcaption></figure>

**Step 2.** Paste a hash of a transaction that matches your alert's trigger

<figure><img src="../.gitbook/assets/image (55).png" alt=""><figcaption><p>Testing webhook: paste the transaction hash</p></figcaption></figure>

**Step 3.** Click "**Test Webhook**" to confirm and send the test event.

Your webhook will be invoked with the transaction corresponding to the hash you pasted, and **event\_type** of `TEST`. You'll be presented with overview of that execution.

<figure><img src="../.gitbook/assets/image (57).png" alt=""><figcaption><p>Result of a manual (test) execution of a webhook</p></figcaption></figure>

