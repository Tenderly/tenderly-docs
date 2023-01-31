# 📣 General Info

[**Tenderly**](https://tenderly.co/) is an all-in-one **Web3 development platform** that accelerates smart contract development by combining debugging tools with observability and blockchain node infrastructure. The Tenderly platform provides a fully integrated experience that enables developers to build, test, monitor, and operate smart contracts in one place.&#x20;

{% hint style="success" %}
We recently had a rather big release, which includes:

* [**Web3 Gateway**](web3-gateway/)
* [**Web3 Actions**](web3-actions/intro-to-web3-actions.md)
* [**War Room Aid Kit**](debugger/war-room-aid-kit.md)
* [**Tenderly Sandbox**](tenderly-sandbox.md)
* [**Debugger Chrome Extension**](debugger/tenderly-debugger-extension.md)

\
You can read more about it right here :point\_down:
{% endhint %}

{% embed url="https://blog.tenderly.co/new-features-web3-actions-war-rooms-sandbox-debugger-extension/" %}

****[**Tenderly Web3 Gateway**](web3-gateway/)****

Use Tenderly's production node to read, stream, and analyze blockchain data with 100% consistency and up to eight times faster read-heavy workloads. Tenderly Web3 Gateway is the first node as a service that enables you to [run transaction simulations using a single RPC URL](web3-gateway/references/simulate-json-rpc.md) thanks to a custom RPC endpoint.&#x20;

Eliminate the node infrastructure overhead and focus on building your dapps with a high level of reliability, quality, and predictability.&#x20;

{% embed url="https://blog.tenderly.co/introducing-web3-gateway-to-all-in-one-developer-platform/" %}

[**Contract Verification**](https://docs.tenderly.co/monitoring/contract-verification)

Contract verification is an essential step in enabling Debugger, Transaction Simulator, Web3 Actions, and other Tenderly features and ensuring they work seamlessly with your smart contracts. Tenderly offers several methods of verification, bringing different levels of control, visibility, and flexibility.

{% content-ref url="monitoring/smart-contract-verification/" %}
[smart-contract-verification](monitoring/smart-contract-verification/)
{% endcontent-ref %}

****[**Transaction** **Simulator**](simulations-and-forks/how-to-simulate-a-transaction/)****

Know how your transactions will behave before you execute them, estimate the gas usage, and test potential bug fixes. **You will find extensive Simulation API documentation with use cases, code examples, and our GitHub repo on the following link:**

{% content-ref url="simulations-and-forks/simulation-api/" %}
[simulation-api](simulations-and-forks/simulation-api/)
{% endcontent-ref %}

[**Web3 Actions**](web3-actions/intro-to-web3-actions.md)

Run your code in response to on-chain (or even off-chain) events, usually on your smart contracts.

You can use Web3 Actions to create custom scenarios to further deepen your debugging process, create alerting patterns that are not available out-of-the-box in the [**Alerting**](broken-reference) section, automate testing or live production execution in [**Simulator**](simulations-and-forks/how-to-simulate-a-transaction/) and [**Forks**](simulations-and-forks/how-to-create-a-fork/), or anything else that comes to (your) mind.

[**Wallet Monitoring**](monitoring/wallets/)

Use all Tenderly features with any wallet address!

****[**Transaction Filtering**](monitoring/contracts/#transaction-filtering)****

Sort and group transactions by any parameter you want and make it easier to explore and analyze robust data.

[**Visual Debugger**](debugger/how-to-use-tenderly-debugger/)

Inspect the transaction execution with a couple of clicks and instantly find the line your transaction reverted on.

[**State Inspector**](debugger/how-to-use-tenderly-debugger/#decoded-state-changes)

See the state of your contract at any point in a transaction and explore state changes in a granular view.

[**Smart Contract Analytics**](analytics/general-analytics.md)

Visualize and analyze the behavior of your smart contract to spot patterns and gain a deeper insight into transaction data.

[**Real-time Alerting**](broken-reference)

Any time an event triggers your custom set of rules you will receive a notification on your favorite channels like Slack, Email, PagerDuty, etc.

****[**Gas Profiler**](debugger/how-to-use-tenderly-debugger/#gas-profiler)****

Get a granular gas usage breakdown to help you optimize your smart contracts and lower the gas cost of your transactions.

[**Forks**](simulations-and-forks/how-to-create-a-fork/)

Take your simulations a step further by creating a temporary fork of any supported network and execute multiple transactions in a row to test their behavior.

[**Integrations**](monitoring/integrations.md)

Use our powerful API to access real-time blockchain data necessary for your business. Integrate Tenderly with your product to deliver more value faster.
