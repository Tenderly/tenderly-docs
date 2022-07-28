# Event Emit

![](<../../.gitbook/assets/Creating an Alert - Event Emmited.png>)

#### Introduction

This alert type triggers whenever a specific event is emitted in one of your contracts.

#### Example

Let’s get notified every time a spender is granted rights to withdraw tokens from an owner.

![](<../../.gitbook/assets/Creating an Alert - Event Emitted Network.png>)

* Add an ERC20 Smart Contract to Project. You can see here how to [**Add a new contract**](../../monitoring/smart-contracts/) to your Project.
* Go to **Alerting** in the side navigation **—>** **New Alert** **—>** **Event Emit —> Address —> Select Address —>** Find the ERC20 Smart Contract **—>**Choose the contract **—>** Choose the **Approval** event **—> Next —>** Choose an Alert Destination **—> Save.**
* Once done, you'll get a notification whenever a call to [approve](https://docs.openzeppelin.com/contracts/2.x/api/token/erc20#IERC20-approve-address-uint256-) sets the spender allowance for an owner.
* After creating an Alert, you can further customize it by changing its name, writing a description, setting a level, and adding more destinations. You can do this by [editing the Alert in a few steps](https://docs.tenderly.co/alerts/creating-an-alert/editing-an-alert). &#x20;
