# 🗺 Supported Networks & Languages

{% tabs %}
{% tab title="Networks" %}
<img src=".gitbook/assets/image (80) (1) (1).png" alt="" data-size="line"> Mainnet

<img src=".gitbook/assets/image (85) (1) (1).png" alt="" data-size="line"> Kovan

<img src=".gitbook/assets/image (73).png" alt="" data-size="line"> Ropsten

<img src=".gitbook/assets/image (75) (1) (1).png" alt="" data-size="line"> Rinkeby

<img src=".gitbook/assets/image (74) (1) (1).png" alt="" data-size="line"> Gorli

<img src=".gitbook/assets/image (83) (1) (1) (1).png" alt="" data-size="line"> RSK

<img src=".gitbook/assets/image (71).png" alt="" data-size="line"> RSK Testnet

<img src=".gitbook/assets/image (82) (1) (1).png" alt="" data-size="line"> BSC

<img src=".gitbook/assets/image (88) (1) (1).png" alt="" data-size="line"> BSC Testnet

<img src=".gitbook/assets/image (86) (1) (1).png" alt="" data-size="line"> POA

<img src=".gitbook/assets/image (84) (1) (1).png" alt="" data-size="line"> xDai

<img src=".gitbook/assets/image (69).png" alt="" data-size="line"> Polygon

<img src=".gitbook/assets/image (70) (1).png" alt="" data-size="line"> Polygon Mumbai

<img src=".gitbook/assets/image (87) (1) (1).png" alt="" data-size="line"> Optimistic Ethereum

<img src=".gitbook/assets/image (72).png" alt="" data-size="line"> Optimistic Kovan

<img src=".gitbook/assets/image (81) (1).png" alt="" data-size="line"> Avalanche C-Chain

<img src=".gitbook/assets/image (79) (1).png" alt="" data-size="line"> Avalanche C-Chain Fuji

<img src=".gitbook/assets/image (77) (1).png" alt="" data-size="line"> Fantom

<img src=".gitbook/assets/image (78) (1).png" alt="" data-size="line"> Fantom Testnet

<img src=".gitbook/assets/image (82).png" alt="" data-size="line"> Arbitrum\*

<img src=".gitbook/assets/image (83).png" alt="" data-size="line"> Arbitrum Testnet\*
{% endtab %}

{% tab title="Languages" %}
<img src=".gitbook/assets/logo.svg" alt="" data-size="line"> Solidity

<img src=".gitbook/assets/vyper-logo-square.png" alt="" data-size="line"> Vyper
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
