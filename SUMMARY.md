# Table of contents

* [General Info](README.md)
* [Supported Networks](getting-started/README.md)
  * [Local Network Support](getting-started/creating-an-account.md)
* [Supported Languages](project.md)
* [Pricing](pricing/README.md)
  * [Billing](pricing/billing.md)
* [Projects](projects/README.md)
  * [Private Projects](projects/private-projects.md)
  * [Organization Projects](projects/organization-projects.md)
* [Teams & Collaboration](teams-and-collaboration/README.md)
  * [Sharing](teams-and-collaboration/sharing.md)
  * [Collaborators](teams-and-collaboration/collaborators.md)
  * [Organizations](teams-and-collaboration/organizations.md)
* [Explorer](explorer.md)

## Tenderly API

* [Authenticating with the Tenderly API](tenderly-api/authenticating-with-the-tenderly-api.md)
* [Transaction Search API](tenderly-api/transaction-search-api.md)
* [Analytics API](tenderly-api/analytics-api.md)
* [Trace API](tenderly-api/trace-api.md)
* [Alerting API](tenderly-api/alerting-api.md)
* [Simulation(s) API](tenderly-api/simulation-s-api.md)
* [Smart Contract Management API](tenderly-api/smart-contract-management-api.md)
* [Transaction Information API](tenderly-api/transaction-information-api.md)
* [Synthetix API](tenderly-api/synthetix-api.md)
* [Account Tokens API](tenderly-api/account-tokens-api.md)
* [InstaDapp Simulate API](tenderly-api/instadapp-simulate-api.md)

## Alerts

* [Webhook Notifications](alerts/alerting/README.md)
  * [Rule Types](alerts/alerting/rule-types.md)
  * [Alert Targets](alerts/alerting/alert-targets/README.md)
    * [Configuring Alert Destinations](alerts/alerting/alert-targets/configuring-alert-destinations/README.md)
      * [Email](alerts/alerting/alert-targets/configuring-alert-destinations/email.md)
      * [Slack](alerts/alerting/alert-targets/configuring-alert-destinations/slack.md)
      * [Telegram](alerts/alerting/alert-targets/configuring-alert-destinations/telegram.md)
      * [Discord](alerts/alerting/alert-targets/configuring-alert-destinations/discord.md)
      * [Sentry](alerts/alerting/alert-targets/configuring-alert-destinations/sentry.md)
      * [PagerDuty](alerts/alerting/alert-targets/configuring-alert-destinations/pagerduty.md)
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
  * [Evaluate Expression](alerts/creating-an-alert/evaluate-expression.md)

## Monitoring

* [Transaction Overview](monitoring/contracts/README.md)
  * [Execution Overview](monitoring/contracts/execution-overview/README.md)
    * [Contracts](monitoring/contracts/execution-overview/contracts.md)
    * [Events](monitoring/contracts/execution-overview/events.md)
    * [State Changes](monitoring/contracts/execution-overview/state-changes.md)
    * [Stack Traces (Debugger)](monitoring/contracts/execution-overview/debugger.md)
    * [Gas Profiler](monitoring/contracts/execution-overview/gas-profiler.md)
  * [Transaction Filtering](monitoring/contracts/transaction-filtering.md)
* [Smart Contracts](monitoring/smart-contracts/README.md)
  * [Public Contracts](monitoring/smart-contracts/public-contracts.md)
  * [Private/Local Contracts](monitoring/smart-contracts/private-local-contracts/README.md)
    * [Verifying Private Contracts](monitoring/smart-contracts/private-local-contracts/verifying-private-contracts.md)
  * [Adding a Contract to your Project](monitoring/smart-contracts/adding-a-contract-to-your-project.md)
  * [Using CLI to create a Project and push your Smart Contracts to Tenderly](monitoring/smart-contracts/using-cli-to-create-a-project-and-push-your-smart-contracts-to-tenderly.md)
  * [Proxy Contracts](monitoring/smart-contracts/proxy-contracts.md)
* [Wallets](monitoring/wallets/README.md)
  * [Converting Contracts into Wallets](monitoring/wallets/converting-contracts-into-wallets.md)
  * [Wallet Public Page](monitoring/wallets/wallet-public-page.md)

## Simulations & Forks

* [How to Simulate a Transaction](simulations-and-forks/how-to-simulate-a-transaction/README.md)
  * [Transaction Parameters](simulations-and-forks/how-to-simulate-a-transaction/transaction-parameters.md)
* [How to Create a Fork](simulations-and-forks/how-to-create-a-fork/README.md)
  * [How to set up Metamask with Tenderly](simulations-and-forks/how-to-create-a-fork/how-to-set-up-metamask-with-tenderly.md)
  * [Tenderly Fork API](simulations-and-forks/how-to-create-a-fork/tenderly-fork-api.md)
  * [Chain Simulations](simulations-and-forks/how-to-create-a-fork/chain-simulations.md)
  * [Custom RPC API](simulations-and-forks/how-to-create-a-fork/custom-rpc-api.md)
  * [Tenderly RPC (with HardHat)](simulations-and-forks/how-to-create-a-fork/tenderly-rpc-with-hardhat.md)
  * [Optimizations](simulations-and-forks/how-to-create-a-fork/optimizations.md)
* [Verifying a Smart Contract](simulations-and-forks/verifying-a-smart-contract.md)
* [Edit Contract Source](simulations-and-forks/edit-contract-source.md)
* [Custom Contracts (Import ABI)](simulations-and-forks/custom-contracts-import-abi.md)
* [Integrations](simulations-and-forks/integrations/README.md)
  * [HardHat](simulations-and-forks/integrations/hardhat/README.md)
    * [How to set up Hardhat](simulations-and-forks/integrations/hardhat/how-to-set-up-hardhat.md)
    * [How to install Tenderly and integrate it with Hardhat](simulations-and-forks/integrations/hardhat/how-to-install-tenderly-and-integrate-it-with-hardhat.md)
    * [How to deploy your contracts via ethers.js](simulations-and-forks/integrations/hardhat/how-to-deploy-your-contracts-via-ethers.js.md)
    * [How to use the \`tenderly export\` command to debug and profile local transactions](simulations-and-forks/integrations/hardhat/how-to-use-the-tenderly-export-command-to-debug-and-profile-local-transactions.md)
    * [How to push and verify Smart Contracts with the hardhat-tenderly tasks](simulations-and-forks/integrations/hardhat/how-to-push-and-verify-smart-contracts-with-the-hardhat-tenderly-tasks.md)
    * [How to push and verify Smart Contracts directly through code](simulations-and-forks/integrations/hardhat/how-to-push-and-verify-smart-contracts-directly-through-code.md)
    * [How to use Hardhat and Tenderly to monitor and debug your BSC Smart Contracts](simulations-and-forks/integrations/hardhat/how-to-use-hardhat-and-tenderly-to-monitor-and-debug-your-bsc-smart-contracts.md)
  * [Truffle](simulations-and-forks/integrations/truffle.md)
  * [Brownie](simulations-and-forks/integrations/brownie.md)
  * [Docker](simulations-and-forks/integrations/docker.md)

## Debugger

* [How to use Tenderly Debugger](debugger/how-to-use-tenderly-debugger/README.md)
  * [Transaction Overview](debugger/how-to-use-tenderly-debugger/transaction-overview.md)
  * [Stack Traces](debugger/how-to-use-tenderly-debugger/stack-traces.md)
  * [Decoded Events/Logs](debugger/how-to-use-tenderly-debugger/decoded-events-logs.md)
  * [Decoded State Changes](debugger/how-to-use-tenderly-debugger/decoded-state-changes.md)
* [Gas Profiler](debugger/gas-profiler.md)
* [Exporting a Local Transaction](debugger/exporting-a-local-transaction.md)

## Analytics

* [General Analytics](analytics/general-analytics.md)
* [Custom Queries](analytics/custom-queries.md)
* [Custom Scripts](analytics/custom-scripts.md)

***

* [🤔 FAQ](faq.md)

## Other

* [💻 CLI Documentation](https://docs.tenderly.co/cli)
* [👷 Hardhat Plugin](https://github.com/Tenderly/hardhat-tenderly)
* [🚀 API Documetnation](https://docs.tenderly.co/api)
* [🤓 Privacy Policy](https://tenderly.co/privacy-policy)

***

* [リックロール](https://youtu.be/mW61VTLhNjQ?t=47)
