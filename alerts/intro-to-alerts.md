---
description: >-
  Alerts allow you to listen for on-chain events and receive notifications when
  they occur in a place most convenient for you and your team, like email,
  Slack, or PageDuty.
---

# Intro to Alerts



{% hint style="success" %}
**🎉 Webhooks released!**

You can now send Alert data to a webhook destination in real time and connect different external services and applications. Explore [**how webhooks work** ](configuring-alert-destinations.md#webhooks)and [**how to integrate webhooks into your project**](how-to-use-webhooks-for-alerting.md).
{% endhint %}

Tenderly Alerting listens for events on the blockchain and sends real-time notifications to your desired destination when the event occurs. This can be email, your favorite messaging app, an incident monitoring system, or webhooks and Web3 Actions.

With Tenderly Alerting, you can stay informed about desired or undesired events related to transitions, wallets, smart contracts, or any other activity on the network. This enables you to identify and resolve smart contract transaction issues faster. Alerts can also aid in the early detection of operational, code, or security issues.

Follow these quick links to skip ahead and get started with Tenderly Alerting:

* [**Quickstart guide**](https://docs.tenderly.co/alerts/creating-an-alert)
* ****[**How to set up webhooks for alerting**](https://app.gitbook.com/o/-LeLQOwIQG3HndcULLU2/s/-LeLQaB11\_TIOtLg8tIW/\~/changes/Shs2UGDb7654qHKsjykR/alerts/how-to-use-webhooks-for-alerting)****
* ****[**Alert triggers**](rule-types.md) **and** [**targets**](alert-targets.md)****
* [**Alert destinations**](https://docs.tenderly.co/alerts/alerting/alert-targets/configuring-alert-destinations)

{% embed url="https://www.youtube.com/watch?v=I9XeubHXnIA" %}

## Anatomy of an Alert

Each Alert requires three elements to be configured before it can be enabled:

* **Alert Type:** On-chain event that triggers Tenderly to send you a notification. There are 12 alert trigger types to choose from.
* **Alert Target:** Addresses you want Tenderly to monitor, as well as other settings such as the network, project, and tags.
* **Alert Destination:** Service for receiving notifications about a specific event. One Alert can send notifications to multiple destinations. There are 8 destination types where you can send and receive notifications.

## Alert trigger types overview

Below is a list of all the Alert Types and a brief example of a common use case. Click the link to explore each trigger type in more detail.

| Trigger type                                                                                       | Explanation                                                                                                                                                                                                                              |
| -------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Successful Transaction](https://docs.tenderly.co/alerts/creating-an-alert/successful-transaction) | Notifies you when a successful transaction happens. This is useful when you want to observe transactions from a wallet, dapp, or smart contract getting added to the blockchain.                                                         |
| [Failed Transaction](creating-an-alert/failed-transaction.md)                                      | Send a notification when a transition fails, allowing you to keep track of all the unsuccessful transitions and detect issues, as well as catch malfunctions with your dapp or smart contract early.                                     |
| [Function Call](creating-an-alert/function-call.md)                                                | Fires when a specific function is called from a contract, which is useful for monitoring the execution of smart contracts for potential issues.                                                                                          |
| [Event Emitted](https://docs.tenderly.co/alerts/creating-an-alert/successful-transaction)          | Triggers when a specific event is emitted from a contract. For example, this trigger can be used to monitor every time a spender is approved to transfer tokens on behalf of the owner.                                                  |
| [Event Parameter](https://docs.tenderly.co/alerts/creating-an-alert/event-parameter)               | Alerts you when an event parameter has a particular value. You can use this Alert trigger to monitor when a particular address is approved to transfer tokens on behalf of the owner.                                                    |
| [ERC20 Token Transfer](https://docs.tenderly.co/alerts/creating-an-alert/erc20-token-transfer)     | Triggers when an ERC20 transfer event is emitted from a contract, allowing you to track when you or someone moves tokens. This can be useful for monitoring suspicious wallets during or after an exploit.                               |
| [Allowlisted callers](creating-an-alert/whitelisted-callers.md)                                    | Notifies you when an address that is not on this list calls your smart contract. This Alert can be used for monitoring if an address outside the “allowed” list attempts to call a function that’s reserved only for specific addresses. |
| [Blocklisted Callers](creating-an-alert/blacklisted-callers.md)                                    | Notifies you whenever an address from this list calls your contracts.                                                                                                                                                                    |
| [ETH Balance](creating-an-alert/eth-balance.md)                                                    | Triggers when the ETH balance of an address falls below a threshold. If you are a member of a DAO that is governed by a smart contract, you can set up this alert to notify you when the DAO's balance falls below a certain threshold.  |
| [Transaction Value](creating-an-alert/transaction-value.md)                                        | Notifies you when a transaction value matches set conditions. This alert is useful in situations when a transaction with more than a certain amount of ETH calls a contract.                                                             |
| [State Change](creating-an-alert/state-change.md)                                                  | Fires when a state variable in a contract changes. This alert is ideal for monitoring when the number of required confirmations for a multisig wallet goes below a certain number.                                                       |
| [View Function](creating-an-alert/view-function.md)                                                | Alerts you when a view function's return value matches certain criteria, passes a threshold, or changes by a certain percentage. For instance, this Alert can be used if you want to check the ERC20 balance threshold.                  |

## Alert Destinations overview

All these alert triggers can be configured to send real-time notifications to a place where it’s convenient for your team.

Receive notifications in your favorite messaging app:

* **Email**
* **Slack**
* **Telegram**
* **Discord**

Send alert data to other Tenderly systems:

* **Web3 Actions**
* **Webhooks**

Send alert data to third-party incident and error monitoring platforms like:

* **Sentry**
* **PagerDuty**

Learn [how to set up each Alert Destination](https://docs.tenderly.co/alerts/alerting/alert-targets/configuring-alert-destinations) here.

## What can you do with Tenderly Alerting?

Tenderly Alerting offers value in a variety of circumstances. Whenever you require a dependable alerting system for on-chain activities that can notify you of potential risks or threats, you can rely on Tenderly Alerting.

* **Monitor on-chain activity:** Alerts can be used as a monitoring tool to track user activity on smart contracts, such as failed or successful transactions or state changes. This is useful in scenarios when you need to keep track of specific events or changes in the blockchain environment.
* **Detect suspicious behavior:** Alerts can inform you about suspicious behavior on your smart contracts or wallets, such as security breaches or fraudulent activity. This helps you to take appropriate action to protect your assets and prevent losses.
* **Respond faster in emergency situations:** Alerts also help you detect errors, security issues, or failed transactions. This is useful in situations when you need to take action to resolve a problem immediately after it happens.
* **Ensure greater visibility for your team:** You can configure each Alert to your specifications, including setting the location for notifications convenient for your team.
* **Enable automated processes:** Use Alerts as triggers for Web3 Actions to build custom automated processes that allow you to react automatically to on-chain events with custom code.
