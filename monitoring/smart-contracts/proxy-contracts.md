# Proxy Contracts

{% hint style="info" %}
When simulating a transaction with a proxy contract, Tenderly will show all of the functions from both the proxy and the contract it delegates to for easier debugging and editing code.
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
