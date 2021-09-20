---
description: 'What are Tenderly Alerts, how do they work and how to set them up.'
---

# Webhook Notifications

## The Problem

In traditional development, your software is your system, so everything that is happening inside of that system is of interest to you. Then came Blockchain, and there is this huge paradigm shift where your software \(Smart Contracts\) is just a part of an ever-expanding system whose parts are continuously interacting with each other.

All of this noise makes it hard to see what is happening with your Smart Contracts. What’s even scarier is that if you don’t actively monitor your Smart Contracts, you’ll probably miss some critical activity that happened during execution.

## The Solution

With Tenderly you can set up custom real-time alerts and get notified when anything of your interest happens on the Ethereum Blockchain in just a few clicks.

We run our own full nodes meaning that we process the blockchain in real-time. So you can set up to receive alert notifications in real-time or at any interval that fits your need \(every 15 min, etc.\).

Tenderly integrates with your favourite apps and services. Each integration offers features that help track your Alerts.

![](../../.gitbook/assets/image%20%2812%29.png)

{% hint style="warning" %}
#### All destinations are shared account-wide on all projects. If you edit or delete a destination it will be applied to all projects and active rules. Check out how to [configure Alert destinations here.](alert-targets/configuring-alert-destinations/)
{% endhint %}

This is the list of alert types Tenderly provides:

![](../../.gitbook/assets/image%20%2813%29.png)



* **Successful Transaction** - Get notified if a transaction has succeeded
* **Failed Transaction** - Get notified if a transaction has failed
* **Whitelisted Callers** - Get notified if an unknown address calls your Smart Contract
* **Blacklisted Callers** - Get notified if a specific address from the blacklist calls your Smart Contract
* **Function Call** - Get notified if a specific function gets called in a transaction
* **SC Caller** - Get alerted if another Smart Contract calls your Smart Contract
* **Specific** - Get alerted when a function is called with a specific argument
* **Compare** - Use operators like greater than, equal, etc. to compare function arguments

