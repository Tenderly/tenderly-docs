# Blacklisted Callers

![](<../../.gitbook/assets/Blacklisted-Callers (1).gif>)

#### Introduction

Triggers whenever an address from this list calls one of your contracts.

#### Example 1

This one is one of the favourite security-oriented alerts: **we can get a notification whenever someone who isn’t whitelisted calls our contract**.

For this example, I’ve set up a simple Gnosis Multisig Wallet which you can [find here](https://dashboard.tenderly.co/contract/kovan/0xbcf55f198e2a5ff4c632610183b1a5290c193e4a).

Now, whenever someone other then the owners of the Multisig Wallet calls this Smart Contract I’ll get an e-mail instantly so that I can react accordingly.

* First things first: add the contract to a Project either via the tenderly push command or using the Verified contract feature.\

* Go to the alerts tab, select the **Whitelisted Callers** rule, and then select the **MultiSigWalletWithDailyLimit** Smart Contract.\

* I’ve added the following addresses to the whitelist (the owners of the Multisig wallet): **0xc9E094Deb826b00D10af0aB3D2A62d712e89F67A **and** 0xC4dFd227848Fbe6640ab14c9C339845BEd350665.**

Tenderly has a smart delivery algorithm for the e-mails we send your way. You will get notified instantly when something happens, and afterward, you will receive aggregated notifications when it makes more sense, so the spam will be on a bare minimum if any. So you’ll have both the latest alerts from Tenderly and the latest and greats from Netflix at the top of your inbox!

#### Example 2

Let’s get notified every time when blacklisted address calls contracts from our Project.

*   First of all, we need to add Smart Contract to Project. You can see here how to **\[Add new contract]** into Project.


* Click on **Alerting** in the navigation **—>** **New Alert** **—>** **Blacklisted Callers —> Project —>** Paste the address you want to blacklist and click the **Add** button **—> Next —>** Choose Alert Destination **—> Save.**\
  ****
* That’s it! You'll receive a notification whenever blacklisted addresses call for contracts from our project.\

* When Alert was created if we want to add a description, alert level, more alert destinations, or change the name, we can do that. You can see how in [Edit Alert](editing-an-alert.md).
