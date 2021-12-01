# Rule Types

This is the list of alert types that Tenderly provides:

![](<../../.gitbook/assets/Screenshot 2021-10-21 at 10.36.34.png>)

****[**Successful Transaction**](../creating-an-alert/successful-transaction.md) - great for monitoring low-traffic addresses such as multi-sigs and to check on the heartbeat of your system.

****[**Failed Transaction**](../creating-an-alert/failed-transaction.md) - get notified when a transaction fails, great for discovering unknown bugs.

****[**Function Call**](../creating-an-alert/function-call.md) - get notified when a specific function is called, both as a part of the top level transaction or as an internal call; great when you don't have an event you can use for the alerting.

****[**Event Emitted**](../creating-an-alert/event-emit.md) - get notified when a specific event is emitted.

****[**Event Parameter**](../creating-an-alert/event-parameter.md) - get notified if an Event parameter matches a certain criteria.

****[**ERC20 Token Transfer**](../creating-an-alert/erc20-token-transfer.md) - get notified when a certain token is sent to or from your address.

****[**Whitelisted Callers**](../creating-an-alert/whitelisted-callers.md) - get notified when anyone who is not on the list calls a specific contract (good for multi-sigs and DAOs).

****[**Blacklisted Callers**](../creating-an-alert/blacklisted-callers.md) **** - get notified when anyone from this list call a specific contract (good for matching knows malicious addresses).

****[**ETH Balance**](../creating-an-alert/eth-balance.md) - get notified when your ETH balance (or a native chain's currency) falls under a certain threshold (good for Bots, Keepers and Oracles).

****[**Transaction Value**](../creating-an-alert/transaction-value.md) - get notified when a transaction value matches a certain criteria.

****[**State Change**](../creating-an-alert/state-change.md) - get notified when a _state change_ matches a certain criteria, passes a threshold or changes by a certain percentage.

****[**View Function**](../creating-an-alert/view-function.md) - get notified when a view function's _return value_ matches a certain criteria, passes a threshold or changes by a certain percentage.
