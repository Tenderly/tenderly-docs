---
description: Learn about the pricing models and rate limits for DevNets.
---

# Pricing

DevNet pricing is based on a tiered structure that offers different levels of access and features to meet your needs. Usage is measured using Tenderly Units (TUs), which are allocated for different operations within the DevNet environment.

{% hint style="success" %}
During the initial DevNet release period, you don’t have to worry about rate limits – there are none. So, [head over to the Dashboard](https://dashboard.tenderly.co/register?redirectTo=devnets) and start experimenting!
{% endhint %}

### **Pricing tiers**

| Free              | Developer              | Pro                     |
| ----------------- | ---------------------- | ----------------------- |
| 1 DevNet template | 5 DevNet templates     | 100 DevNet templates    |
| Sequential runs   | 5 active parallel runs | 15 active parallel runs |
| /                 | /                      | Teams & Personal runs   |

### **Tenderly Units (TUs) Usage**

[Reference this doc ](https://docs.tenderly.co/web3-gateway/pricing)to understand what is considered Read, Compute, and Write.

| ETH Methods    | Reads | Computes | Writes |
| -------------- | ----- | -------- | ------ |
| Tenderly Units | 4 TU  | 16 TU    | 80 TU  |

The total TU limits are as follows:

* **Free plan:** 25M TUs
* **Paid plans:** 100M TUs

{% hint style="info" %}
DevNets feature TU-based restrictions, allowing you to perform up to **300 tests (runs) per day**, even on the most complex files. In general, developers usually conduct a much smaller number of tests on a daily basis. When a project is in active development, we see spikes of up to 100 tests, so this enhanced limit will surely meet your requirements.
{% endhint %}
