# Alert Targets

To set up an alert target, we'll first choose the [KyberNetworkProxy](https://dashboard.tenderly.co/contract/main/0x818e6fecd516ecc3849daf6845e3ec868087b755?utm\_source=blog\&utm\_medium=post\&utm\_campaign=10\_ways\&utm\_content=kyber\_network\_contract) as an example. Next, we need to pick the event and the parameter we want to use for this alert:

![](<../.gitbook/assets/Creating an Alert 1.png>)

![](<../.gitbook/assets/Creating an Alert 2.png>)

Note that you can also target your Smart Contracts by network or project. This granulation is very useful for [the **Failed Transaction** alert type](https://docs.tenderly.co/alerts/creating-an-alert/failed-transaction).

We're going to pick the **ExecuteTrade** event and the **actualSrcAmount** parameter. Finally, we're going to select the **>=** (Greater than or equal) comparator and input **1000** as the comparison value:

![](<../.gitbook/assets/image (26) (1).png>)

{% hint style="info" %}
**Note**: Thanks to the addition of [**Wallet**](../monitoring/wallets/) support to Tenderly, we now have a new parameter when adding alert targets which are _**addresses**_ instead of previously _contracts_.
{% endhint %}

![](<../.gitbook/assets/Creating an Alert 3.png>)
