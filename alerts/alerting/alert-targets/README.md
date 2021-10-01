# Alert Targets

As the alert target we will be using the [KyberNetworkProxy](https://dashboard.tenderly.co/contract/main/0x818e6fecd516ecc3849daf6845e3ec868087b755?utm_source=blog&utm_medium=post&utm_campaign=10_ways&utm_content=kyber_network_contract) as an example. Next up, we need to pick the event and the parameter we want to use for this alert:

![](../../../.gitbook/assets/image%20%2846%29.png)

Note that you can also target your Smart Contracts by network or project as well. This granulation is very useful for the **Failed Transaction** alert type.

We're going to pick the **ExecuteTrade** event and the **actualSrcAmount** parameter. Finally, we're going to select the **&gt;=** \(Greater than or equal\) comparator and input **1000** as the comparison value:

![](../../../.gitbook/assets/image%20%2826%29.png)



