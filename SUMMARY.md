# Table of contents

* [📣 General Info](README.md)
* [🗺 Supported Networks & Languages](supported-networks-and-languages.md)
* [⚗ Projects](projects.md)
* [🫂 Teams & Collaboration](teams-and-collaboration/README.md)
* [🔍 Explorer](explorer.md)

## 🦅 Monitoring

* [Transaction Overview](monitoring/contracts/README.md)
  * [Execution Overview](monitoring/contracts/execution-overview.md)
  * [Mempool & Simulating Pending Transactions](monitoring/contracts/mempool-and-simulating-pending-transactions.md)
  * [Commenting & Prioritizing Traces](monitoring/contracts/commenting-and-prioritizing-traces.md)
* [Smart Contracts](monitoring/smart-contracts/README.md)
  * [Public Contracts](monitoring/smart-contracts/public-contracts.md)
  * [Proxy Contracts](monitoring/smart-contracts/proxy-contracts.md)
* [Verifying a Smart Contract](monitoring/verifying-a-smart-contract.md)
* [Wallets](monitoring/wallets/README.md)
  * [Converting Contracts into Wallets](monitoring/wallets/converting-contracts-into-wallets.md)
  * [Wallet Public Page](monitoring/wallets/wallet-public-page.md)
  * [Simulations with a Wallet](monitoring/wallets/simulations-with-a-wallet.md)
  * [Wallet Analytics](monitoring/wallets/wallet-analytics.md)
  * [Wallet Tags](monitoring/wallets/wallet-tags.md)
* [Integrations](monitoring/integrations.md)

## 🧩 Web3 Actions

* [Intro to Web3 Actions](web3-actions/intro-to-web3-actions.md)
* [Functions](web3-actions/functions.md)
* [Configuration](web3-actions/configuration.md)
* [Triggers](web3-actions/triggers.md)
* [Networks](web3-actions/networks.md)
* [Notifications](web3-actions/notifications.md)

## 🔔 Alerts

* [Webhook Notifications](alerts/alerting/README.md)
  * [Rule Types](alerts/alerting/rule-types.md)
  * [Alert Targets](alerts/alerting/alert-targets/README.md)
    * [Configuring Alert Destinations](alerts/alerting/alert-targets/configuring-alert-destinations.md)
    * [Custom Webhook](alerts/alerting/alert-targets/custom-webhook.md)
* [Creating an Alert](alerts/creating-an-alert/README.md)
  * [Successful transaction](alerts/creating-an-alert/successful-transaction.md)
  * [Failed Transaction](alerts/creating-an-alert/failed-transaction.md)
  * [Function Call](alerts/creating-an-alert/function-call.md)
  * [Event Emit](alerts/creating-an-alert/event-emit.md)
  * [Event Parameter](alerts/creating-an-alert/event-parameter.md)
  * [ERC20 Token Transfer](alerts/creating-an-alert/erc20-token-transfer.md)
  * [Whitelisted Callers](alerts/creating-an-alert/whitelisted-callers.md)
  * [Blacklisted Callers](alerts/creating-an-alert/blacklisted-callers.md)
  * [ETH Balance](alerts/creating-an-alert/eth-balance.md)
  * [Transaction Value](alerts/creating-an-alert/transaction-value.md)
  * [State Change](alerts/creating-an-alert/state-change.md)
  * [View Function](alerts/creating-an-alert/view-function.md)
  * [Editing an Alert](alerts/creating-an-alert/editing-an-alert.md)

## 🔮 Simulations & Forks

* [How to Simulate a Transaction](simulations-and-forks/how-to-simulate-a-transaction/README.md)
  * [Simulation Parameters](simulations-and-forks/how-to-simulate-a-transaction/transaction-parameters.md)
  * [Pending vs Historical Block](simulations-and-forks/how-to-simulate-a-transaction/pending-vs-historical-block.md)
  * [Editing Contract Source](simulations-and-forks/how-to-simulate-a-transaction/editing-contract-source.md)
* [How to Create a Fork](simulations-and-forks/how-to-create-a-fork/README.md)
  * [Fork Parents](simulations-and-forks/how-to-create-a-fork/fork-parents.md)
* [Simulation API Placeholder](simulations-and-forks/simulation-api-placeholder.md)
* [Simulation API](simulations-and-forks/simulation-api/README.md)
  * [Configuration of API access](simulations-and-forks/simulation-api/configuration-of-api-access.md)
  * [Integrations](simulations-and-forks/simulation-api/integrations/README.md)
    * [Instant Staging/QA environment](simulations-and-forks/simulation-api/integrations/instant-staging-qa-environment.md)
    * [CI/CD pipeline for smart contracts](simulations-and-forks/simulation-api/integrations/ci-cd-pipeline-for-smart-contracts.md)
    * [DApp playground mode](simulations-and-forks/simulation-api/integrations/dapp-playground-mode.md)
    * [Dry-run user transactions](simulations-and-forks/simulation-api/integrations/dry-run-user-transactions.md)
  * [Fork Customization](simulations-and-forks/simulation-api/fork-customization/README.md)
    * [How to advance/mine the block](simulations-and-forks/simulation-api/fork-customization/how-to-advance-mine-the-block.md)
    * [How to advance time on Fork](simulations-and-forks/simulation-api/fork-customization/how-to-advance-time-on-fork.md)
    * [Easily debug failed transactions](simulations-and-forks/simulation-api/fork-customization/easily-debug-failed-transactions.md)
    * [How to impersonate any address as a simulation sender](simulations-and-forks/simulation-api/fork-customization/how-to-impersonate-any-address-as-a-simulation-sender.md)
    * [How to point the fork to a specific simulation](simulations-and-forks/simulation-api/fork-customization/how-to-point-the-fork-to-a-specific-simulation.md)
    * [How to specify/change network chain\_id](simulations-and-forks/simulation-api/fork-customization/how-to-specify-change-network-chain\_id.md)
  * [Testing](simulations-and-forks/simulation-api/testing/README.md)
    * [Local tests on top of Mainnet data in the Cloud](simulations-and-forks/simulation-api/testing/local-tests-on-top-of-mainnet-data-in-the-cloud/README.md)
      * [First usage of Tenderly APIs in tests](simulations-and-forks/simulation-api/testing/local-tests-on-top-of-mainnet-data-in-the-cloud/first-usage-of-tenderly-apis-in-tests.md)
      * [A bit of testing infrastructure](simulations-and-forks/simulation-api/testing/local-tests-on-top-of-mainnet-data-in-the-cloud/a-bit-of-testing-infrastructure.md)
    * [How to deploy smart contract once per test execution](simulations-and-forks/simulation-api/testing/how-to-deploy-smart-contract-once-per-test-execution.md)
    * [Deploy smart contracts once per test-suite execution](simulations-and-forks/simulation-api/testing/deploy-smart-contracts-once-per-test-suite-execution.md)
    * [Reset transactions after completing the test](simulations-and-forks/simulation-api/testing/reset-transactions-after-completing-the-test.md)

## 🐞 Debugger

* [How to use Tenderly Debugger](debugger/how-to-use-tenderly-debugger/README.md)
  * [Transaction Overview](debugger/how-to-use-tenderly-debugger/transaction-overview.md)
  * [Investigating a Failed Transaction](debugger/how-to-use-tenderly-debugger/investigating-a-failed-transaction.md)
  * [Investigating a Hack (Cover Protocol)](debugger/how-to-use-tenderly-debugger/investigating-a-hack-cover-protocol.md)
* [Exporting a Local Transaction](debugger/exporting-a-local-transaction.md)

## 📊 Analytics

* [Analytics Overview](analytics/general-analytics.md)

## Other

* [🕹 Tenderly API](https://app.gitbook.com/o/-LeLQOwIQG3HndcULLU2/s/ES8WtN6Gx8HH3zi8low4/)
* [⌨ Tenderly CLI](https://github.com/Tenderly/tenderly-cli)
* [👷 Hardhat Plugin](https://github.com/Tenderly/hardhat-tenderly)
* [💾 Simulation API Rate Limits](other/simulation-api-rate-limits.md)
* [🤓 Privacy Policy](https://tenderly.co/privacy-policy)

***

* [リックロール](https://youtu.be/mW61VTLhNjQ?t=47)
