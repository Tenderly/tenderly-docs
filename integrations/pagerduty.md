---
description: Receive alerts in real-time and act upon them.
---

# PagerDuty

You can connect Tenderly with your PagerDuty workspace and get real-time notifications when an alert rule matches a transaction. Connecting multiple services is also supported so you can route certain rules to specific services.

## How to connect PagerDuty with Tenderly

Navigate to a project and go to the **Alerting** tab.

![](../.gitbook/assets/image%20%283%29.png)

Click on **Destinations.**

![](../.gitbook/assets/image%20%284%29.png)

From the list of available destinations choose **PagerDuty.**

![](../.gitbook/assets/image%20%281%29.png)

Click on **Connect PagerDuty** to be redirected to the PagerDuty install flow.

![](../.gitbook/assets/image.png)

After entering your credentials you will be prompted to select services you would like to integrate with.

![](../.gitbook/assets/image%20%285%29.png)

Select the services and click on **Connect** to finalize the connection. This will redirect you back to the Tenderly Dashboard, and PagerDuty should be listed in the **Active Destinations** section.

![](../.gitbook/assets/image%20%287%29.png)

And that's it! Now when a transaction matches a configured alert rule you will get an incident report instantly delivered to your PagerDuty service.

![](../.gitbook/assets/image%20%282%29.png)

