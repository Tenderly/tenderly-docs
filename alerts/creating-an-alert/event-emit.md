# Event Emit

![](../../.gitbook/assets/Event-Emit.gif)

#### Introduction

Triggers whenever a specific event is emitted in one of your contracts.

#### Example

Let’s get notified every time when a spender is granted rights to withdraw tokens from an owner.

* First of all, we need to add some ERC20 Smart Contract to Project. You can see here how to [**Add a new contract**](../../monitoring/smart-contracts/) into your Project.\

* Click on **Alerting** in the navigation **—>** **New Alert** **—>** **Event Emit —> Contract —> Select Contract —>** Find ERC20 Smart Contract and Choose it **—>** Choose **Approval** event **—> Next —>** Choose Alert Destination **—> Save.**\
  ****
* That’s it! You’ll get a notification whenever the allowance of a spender for an owner is set by a call to [approve](https://docs.openzeppelin.com/contracts/2.x/api/token/erc20#IERC20-approve-address-uint256-).\

* When Alert was created if we want to add a description, alert level, more alert destinations, or change the name, we can do that. You can see how in [Edit Alert](editing-an-alert.md).
