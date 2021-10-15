# Transaction Parameters

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 09.18.09.png>)

If you use Custom Contract selector you can simulate a custom contract execution by pasting your contract data or importing your contract ABI. 

Otherwise, choose a public contract from your project (or add any public contract to your project before selecting it).

{% hint style="success" %}
[Read more about editing the contract source (on the fly) here](editing-contract-source.md).
{% endhint %}

#### Transaction Parameters

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 09.18.49.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-15 at 09.16.57.png>)

{% hint style="success" %}
[Read more about using the pending or historical block here](pending-vs-historical-block.md).
{% endhint %}

* Block Number (locked to next block if pending is selected)
* Transaction Index (locked if pending is selected)
* From (Address)
* Gas (Amount)
* Gas Price
* Value (monetary value passed within the transaction, not required)
* Optional Access List (as contract address or by importing a JSON)
  * Announce to the node which contracts you will be using in order to lower the transaction cost
  * Makes sense to be used for greater number of contracts and function calls
  * If the list of contracts changes after the announcement this [optimization](../how-to-create-a-fork/optimizations.md) will not work
