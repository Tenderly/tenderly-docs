# Simulation Parameters

If you use Custom Contract selector you can simulate a custom contract execution by pasting your contract data or importing your contract ABI.&#x20;

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.17.27.png>)

Otherwise, choose a public contract from your project (or add any public contract to your project before selecting it).

{% hint style="success" %}
[Read more about editing the contract source (on the fly) here](editing-contract-source.md).
{% endhint %}

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.24.35.png>)

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.25.27.png>)

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.26.10.png>)

{% hint style="success" %}
[Read more about using the pending or historical block here](pending-vs-historical-block.md).
{% endhint %}

### **General Transaction Parameters**

* Block Number (locked to next block if pending is selected)
* Transaction Index (locked if pending is selected)
* From (Address)
* Gas (Amount)
* Gas Price
* Value (monetary value passed within the transaction, not required)

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.31.23.png>)

### **Optional Access List**

* Announce to the node which contracts you will be using in order to lower the transaction cost
* Makes sense to be used for greater number of contracts and function calls
* If the list of contracts changes after the announcement this optimization will not work

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.32.11.png>)

### State Override

If you want to **change any of the states on the fly**, you can **use the State Override** for any of the contracts you want.&#x20;

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.35.23.png>)

Select either a custom or existing contract in your project and you can change any of its state parameters for the purposes of your simulation.

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.36.38.png>)

You can also add as many State Overrides for any number of contracts you want, just by clicking on the `Add State Override` button:

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.38.52.png>)

If you want to save your simulation starting point with modified State Overrides and other parameters, you can use Forks and our [**Fork Parents feature**](../how-to-create-a-fork/fork-parents.md).
