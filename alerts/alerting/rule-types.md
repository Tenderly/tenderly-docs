# Rule Types

This is the list of alert types that Tenderly provides:

![](<../../.gitbook/assets/Screenshot 2021-10-21 at 10.36.34.png>)

****[**Successful Transaction**](../creating-an-alert/successful-transaction.md): This type of alert is great for monitoring low-traffic addresses such as multi-sigs and checking on the heartbeat of your system.

****[**Failed Transaction**](../creating-an-alert/failed-transaction.md): **** When you choose this solution, you get notified when a transaction fails, which is a great way to discover unknown bugs.

****[**Function Call**](../creating-an-alert/function-call.md): **** This alert type notifies you when a specific function is called, as a part of the top level transaction or as an internal call. This option is great when you don't have an event you can use for alerting.

****[**Event Emitted**](../creating-an-alert/event-emit.md): Choose this alert type to get notified when a specific event is emitted.

****[**Event Parameter**](../creating-an-alert/event-parameter.md): This option notifies you when an Event parameter matches a certain criterion.

****[**ERC20 Token Transfer**](../creating-an-alert/erc20-token-transfer.md): This alert type allows you to get notified when a certain token is sent to or from your address.

****[**Whitelisted Callers**](../creating-an-alert/whitelisted-callers.md): Get notified when anyone who is not on the list calls a specific contract (good for multi-sigs and DAOs).

****[**Blacklisted Callers**](../creating-an-alert/blacklisted-callers.md): This type of alert notifies you when anyone from this list call a specific contract (good for matching known malicious addresses).

****[**ETH Balance**](../creating-an-alert/eth-balance.md): Receive a notification when your ETH balance (or a native chain's currency) falls under a certain threshold (good for Bots, Keepers and Oracles).

****[**Transaction Value**](../creating-an-alert/transaction-value.md): Get notified when a transaction value matches certain criteria with this type of alert.

****[**State Change**](../creating-an-alert/state-change.md): Set up this alert type to get notified when a _state change_ matches a certain criterion, passes a threshold, or changes by a certain percentage.

****[**View Function**](../creating-an-alert/view-function.md): This option notifies you when a view function's _return value_ matches a certain criterion, passes a threshold, or changes by a certain percentage.
