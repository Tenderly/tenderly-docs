# Alert Targets

As the alert target we will be using the [KyberNetworkProxy](https://dashboard.tenderly.co/contract/main/0x818e6fecd516ecc3849daf6845e3ec868087b755) as an example. Next up, we need to pick the event and the parameter we want to use for this alert:

![](<../../../.gitbook/assets/image (46).png>)

Note that you can also target your Smart Contracts by network or project as well. This granulation is very useful for the **Failed Transaction** alert type.

We're going to pick the **ExecuteTrade** event and the **actualSrcAmount** parameter. Finally, we're going to select the **>=** (Greater than or equal) comparator and input **1000** as the comparison value:

![](<../../../.gitbook/assets/image (26).png>)

{% hint style="info" %}
Note - since the addition of [**Wallet**](../../../monitoring/wallets/) support to Tenderly, we now have a new parameter when adding alert targets which are _**addresses**_ instead of previously _contracts_.
{% endhint %}

![](<../../../.gitbook/assets/Screenshot 2021-10-14 at 14.06.16.png>)
