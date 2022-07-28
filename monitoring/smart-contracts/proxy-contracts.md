# Proxy Contracts

{% hint style="info" %}
When simulating a transaction with a proxy contract, Tenderly will show all of the functions from both the proxy and the contract it delegates to for easier [debugging and editing code](../../debugger/how-to-use-tenderly-debugger/).
{% endhint %}

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.17.04.png>)

Proxy contract basically has only one variable, which is the destination address for forwarding your transaction. They are basically used to make contract versioning or bug fixes easier, where if you want to change your smart contract you can do a new deployment without worrying about dependencies, and change just the delivery address in your proxy contract to the newly updated contract.

You can import any contract through the standard flow:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.23.09.png>)

Tenderly will automatically detect a proxy contract and give you the option to add it's latest implementation as well:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.24.23.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.25.05.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.25.42.png>)

You will also be able to see all of the previous (historical) destinations that were set for your proxy contract:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.26.29.png>)

Additionally, if your contract is to be used as a proxy but is not defined by the current industry standards, you are able to convert any contract into a proxy contract:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.28.13.png>)

If you are importing a proxy contract that doesn't conform to one of the two industry standards which Tenderly automatically detects (EIP-1967 and EIP-1167), you can now easily convert that proxy contract to be recognized by the Tenderly platform.

If you are using a different standard than the two mentioned above, you can provide a view function defined on your contract that returns the implementation address. You can also manually set the storage [slot](https://docs.soliditylang.org/en/v0.8.11/internals/layout\_in\_storage.html#layout-of-state-variables-in-storage) containing the implementation address to convert this contract into a Proxy.

![](<../../.gitbook/assets/Screenshot 2022-04-14 at 13.42.06.png>)

Tenderly will list all of the functions which are without parameters and which return `address` as their return type, so you can select a function which returns the implementation for the proxied contract. You can also select the account from which this transaction will be sent, which is important if the proxy contract function you chose has some specific execution rules (e.g. addresses from which it can be called).

![](<../../.gitbook/assets/Screenshot 2022-04-14 at 13.45.17.png>)

![](<../../.gitbook/assets/Screenshot 2022-04-14 at 13.50.05.png>)

You can still use the implementation slot hash to import your proxy contracts by flicking the `use storage slot` switch if that is your preferred way of doing this.
