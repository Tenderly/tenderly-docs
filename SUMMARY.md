# Table of contents

* [📣 General Info](README.md)
* [🗺 Supported Networks & Languages](supported-networks-and-languages.md)
* [⚗ Projects](projects.md)
* [🫂 Teams & Collaboration](teams-and-collaboration/README.md)
* [🔍 Explorer](explorer.md)
* [🪣 Tenderly Sandbox](tenderly-sandbox.md)

## 🔮 Simulations & Forks

* [How to Simulate a Transaction](simulations-and-forks/how-to-simulate-a-transaction/README.md)
  * [Simulation Parameters](simulations-and-forks/how-to-simulate-a-transaction/transaction-parameters.md)
  * [Pending vs Historical Block](simulations-and-forks/how-to-simulate-a-transaction/pending-vs-historical-block.md)
  * [Editing Contract Source](simulations-and-forks/how-to-simulate-a-transaction/editing-contract-source.md)
* [How to Create a Fork](simulations-and-forks/how-to-create-a-fork/README.md)
  * [Fork Parents](simulations-and-forks/how-to-create-a-fork/fork-parents.md)
* [Simulation API](simulations-and-forks/simulation-api/README.md)
  * [Configuration of API Access](simulations-and-forks/simulation-api/configuration-of-api-access.md)
  * [Integration Guides](simulations-and-forks/simulation-api/integration-guides/README.md)
    * [Instant Staging/QA Environment for dApps](simulations-and-forks/simulation-api/integration-guides/instant-staging-qa-environment-for-dapps.md)
    * [CI/CD Pipeline for Smart Contracts](simulations-and-forks/simulation-api/integration-guides/ci-cd-pipeline-for-smart-contracts.md)
    * [dApp Playground Mode](simulations-and-forks/simulation-api/integration-guides/dapp-playground-mode.md)
    * [Dry-run User Transactions](simulations-and-forks/simulation-api/integration-guides/dry-run-user-transactions.md)
  * [Tenderly Fork Customization via API](simulations-and-forks/simulation-api/tenderly-fork-customization-via-api/README.md)
    * [How to Advance/Mine the Block](simulations-and-forks/simulation-api/tenderly-fork-customization-via-api/how-to-advance-mine-the-block.md)
    * [How to Advance Time on Fork](simulations-and-forks/simulation-api/tenderly-fork-customization-via-api/how-to-advance-time-on-fork.md)
    * [Easily Debug Failed Transactions](simulations-and-forks/simulation-api/tenderly-fork-customization-via-api/easily-debug-failed-transactions.md)
    * [How to Impersonate any Address as a Simulation Sender](simulations-and-forks/simulation-api/tenderly-fork-customization-via-api/how-to-impersonate-any-address-as-a-simulation-sender.md)
    * [How to Point the Fork to a Specific Simulation](simulations-and-forks/simulation-api/tenderly-fork-customization-via-api/how-to-point-the-fork-to-a-specific-simulation.md)
    * [How to Specify/Change Network chain\_id](simulations-and-forks/simulation-api/tenderly-fork-customization-via-api/how-to-specify-change-network-chain\_id.md)
    * [How to manage Account Balances in Tenderly Forks](simulations-and-forks/simulation-api/tenderly-fork-customization-via-api/how-to-manage-account-balances-in-tenderly-forks.md)
  * [Testing](simulations-and-forks/simulation-api/testing/README.md)
    * [Local Tests on top of Mainnet Data in the Cloud](simulations-and-forks/simulation-api/testing/local-tests-on-top-of-mainnet-data-in-the-cloud/README.md)
      * [First Usage of Tenderly APIs in Tests](simulations-and-forks/simulation-api/testing/local-tests-on-top-of-mainnet-data-in-the-cloud/first-usage-of-tenderly-apis-in-tests.md)
      * [A bit of Testing Infrastructure](simulations-and-forks/simulation-api/testing/local-tests-on-top-of-mainnet-data-in-the-cloud/a-bit-of-testing-infrastructure.md)
    * [How to Deploy Smart Contract Once per Test](simulations-and-forks/simulation-api/testing/how-to-deploy-smart-contract-once-per-test.md)
    * [Deploy Smart Contracts Once per Test-suite Execution](simulations-and-forks/simulation-api/testing/deploy-smart-contracts-once-per-test-suite-execution.md)
    * [Reset Transactions After Completing the Test](simulations-and-forks/simulation-api/testing/reset-transactions-after-completing-the-test.md)
  * [Simulation API Rate Limits](simulations-and-forks/simulation-api/simulation-api-rate-limits.md)

## 🧩 Web3 Actions

* [Intro to Web3 Actions](web3-actions/intro-to-web3-actions/README.md)
  * [Functions](web3-actions/intro-to-web3-actions/functions.md)
  * [Configuration](web3-actions/intro-to-web3-actions/configuration.md)
  * [Triggers](web3-actions/intro-to-web3-actions/triggers.md)
  * [Networks](web3-actions/intro-to-web3-actions/networks.md)
  * [Notifications](web3-actions/intro-to-web3-actions/notifications.md)
* [How to Handle On-Chain Events](web3-actions/how-to-handle-on-chain-events.md)
* [How to Build a Custom Oracle](web3-actions/how-to-build-a-custom-oracle.md)
* [How to Send a Discord Message About a New Uniswap Pool](web3-actions/how-to-send-a-discord-message-about-a-new-uniswap-pool.md)

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

## 🐞 Debugger

* [How to use Tenderly Debugger](debugger/how-to-use-tenderly-debugger/README.md)
  * [Transaction Overview](debugger/how-to-use-tenderly-debugger/transaction-overview.md)
  * [Investigating a Failed Transaction](debugger/how-to-use-tenderly-debugger/investigating-a-failed-transaction.md)
  * [Investigating a Hack (Cover Protocol)](debugger/how-to-use-tenderly-debugger/investigating-a-hack-cover-protocol.md)
* [Evaluate Expressions with Advanced Debugger](debugger/evaluate-expressions-with-advanced-debugger.md)
* [Exporting a Local Transaction](debugger/exporting-a-local-transaction.md)
* [War Room Aid Kit](debugger/war-room-aid-kit.md)
* [Tenderly Debugger Extension](debugger/tenderly-debugger-extension.md)

## 📊 Analytics

* [Analytics Overview](analytics/general-analytics.md)

## Other

* [🕹 Tenderly API](https://app.gitbook.com/o/-LeLQOwIQG3HndcULLU2/s/ES8WtN6Gx8HH3zi8low4/)
* [⌨ Tenderly CLI](https://github.com/Tenderly/tenderly-cli)
* [👷 Hardhat Plugin](https://github.com/Tenderly/hardhat-tenderly)
* [🐛 Trace API](other/trace-api.md)
* [🤓 Privacy Policy](https://tenderly.co/privacy-policy)

***

* [リックロール](https://youtu.be/mW61VTLhNjQ?t=47)
