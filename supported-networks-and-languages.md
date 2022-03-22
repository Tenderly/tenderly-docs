# 🗺 Supported Networks & Languages

{% tabs %}
{% tab title="Networks" %}
![](<.gitbook/assets/image (80) (1) (1).png>) Mainnet

![](<.gitbook/assets/image (85) (1) (1).png>) Kovan

![](<.gitbook/assets/image (73).png>) Ropsten

![](<.gitbook/assets/image (75) (1) (1).png>) Rinkeby

![](<.gitbook/assets/image (74) (1) (1).png>) Gorli

![](<.gitbook/assets/image (83) (1) (1) (1).png>) RSK

![](<.gitbook/assets/image (71).png>) RSK Testnet

![](<.gitbook/assets/image (82) (1) (1).png>) BSC

![](<.gitbook/assets/image (88) (1).png>) BSC Testnet

![](<.gitbook/assets/image (86) (1).png>) POA

![](<.gitbook/assets/image (84) (1) (1).png>) xDai

![](<.gitbook/assets/image (69).png>) Polygon

![](<.gitbook/assets/image (70) (1).png>) Polygon Mumbai

![](<.gitbook/assets/image (87) (1) (1).png>) Optimistic Ethereum

![](<.gitbook/assets/image (72).png>) Optimistic Kovan

![](<.gitbook/assets/image (81) (1).png>) Avalanche C-Chain

![](<.gitbook/assets/image (79).png>) Avalanche C-Chain Fuji

![](<.gitbook/assets/image (77) (1).png>) Fantom

![](<.gitbook/assets/image (78) (1).png>) Fantom Testnet

![](<.gitbook/assets/image (82).png>) Arbitrum\*

![](<.gitbook/assets/image (83).png>) Arbitrum Testnet\*
{% endtab %}

{% tab title="Languages" %}
![](.gitbook/assets/logo.svg) Solidity

![](.gitbook/assets/vyper-logo-square.png) Vyper
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
\*We decided to split up the **Arbitrum integration** into phases in order to give you (our users) access to Arbitrum on Tenderly as soon as possible, while we finish up the full integration and make all Tenderly features available for Arbitrum.\
\
**Phase 1**, which is now **completed and available for use**, includes the standard EVM implementation without Arbitrum precompiles and custom gas table, which enables the following (for transactions that don’t touch any of the custom precompiles):&#x20;

* [Transaction Debugging ](debugger/how-to-use-tenderly-debugger/)
* [Simulator ](simulations-and-forks/how-to-simulate-a-transaction/)
* [Forks ](simulations-and-forks/how-to-create-a-fork/)



In **Phase 2** we will implement the Arbitrum precompiles which will expand the available feature set:&#x20;

* Transactions listing for single contracts and projects&#x20;
* Alerting&#x20;
* Analytics&#x20;



In **Phase 3** we will mimic the Arbitrum gas usage, which is going to ensure transaction re-execution and enable the Gas Profiler.
{% endhint %}
