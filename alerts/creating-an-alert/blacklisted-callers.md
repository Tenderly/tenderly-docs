# Blocklisted Callers

![](<../../.gitbook/assets/Creating an Alert - Blacklisted Callers 1.png>)

#### Introduction

The Blocklisted Caller alert triggers whenever an address from this list calls one of your contracts. This type of alert is one of the favourite security-oriented alerts because it sends you a **notification whenever someone who isn’t whitelisted calls your contract**.

#### Example 1

For this example, you need to use a [simple Gnosis Multisig Wallet](https://dashboard.tenderly.co/contract/kovan/0xbcf55f198e2a5ff4c632610183b1a5290c193e4a?utm\_source=medium\&utm\_campaign=alerting\_release\&utm\_medium=post\&utm\_content=public\_contract\_listing).

Here are a few guidelines to set up an alert that will notify you whenever someone other than the owners of the Multisig Wallet calls the Smart Contract. Once you receive an email, you can react accordingly.

* First, add the contract to a Project either via the Tenderly push command or using the Verified Contract feature.
* Go to the Alerting tab, select the **Whitelisted Callers** rule, and then select the **MultiSigWalletWithDailyLimit** Smart Contract.
* Add the following addresses to the whitelist (the owners of the Multisig wallet): **0xc9E094Deb826b00D10af0aB3D2A62d712e89F67A** and **0xC4dFd227848Fbe6640ab14c9C339845BEd350665.**

Tenderly has a smart email delivery algorithm. You'll get notified instantly when something of interest happens. Afterward, you'll receive aggregated notifications when suitable, so the spam will be on a bare minimum if any. This way, you’ll receive the latest alerts from Tenderly without missing any other important emails.&#x20;

![](<../../.gitbook/assets/Creating an Alert - Whitelisted Callers 2.png>)

#### Example 2

Here's another example that will help you create an alert that will trigger every time a blocklisted address calls contracts from your Project.

* [Add a new Smart Contract to Projects](https://docs.tenderly.co/monitoring/smart-contracts) through one of the available options.
* Click the **Alerting** tab in the left side bar **—>** **New Alert** **—>** **Blocklisted Callers —> Project —>** Paste the address you want to blocklist & click the **Add** button **—> Next —>** Choose an Alert Destination **—> Save.**
* Start receiving notifications whenever blocklisted addresses call the Smart Contract from your project.
* You have the [option to edit the Alert](https://docs.tenderly.co/alerts/creating-an-alert/editing-an-alert) after setting it up. Feel free to rename it or add a description, alert level, and multiple destinations.
