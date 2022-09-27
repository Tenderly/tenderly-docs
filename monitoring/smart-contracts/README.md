---
description: >-
  Learn how to collect all the contracts you care about so you can monitor,
  debug, and simulate transactions.
---

# Smart Contracts

As a form of an opt-in Smart Contract registry, Tenderly allows you to find any verified public contract and add it to your project. After adding a contract, you can start debugging transactions, doing simulations, or handling more advanced monitoring on the contracts that are important for your project.

To find and add a contract of interest, search for it by name or address. If you can't find the contract you need, it probably means it's not verified. You can still add it to your project to monitor it and verify it later on.&#x20;

There are two options for adding contracts to your project from the Dashboard:

* **Adding a publicly verified contract**. No verification is required. Add a contract by entering its address and choosing the network to which it's deployed. Once added, the contract will show up in the refreshed list of contracts.
* **Adding an unverified contract** to observe in which transactions it's involved. However, these transactions won't be decoded to a human-readable format. Other meaningful information such as state changes, gas usage, and events will also remain in raw form.

{% hint style="info" %}
It's possible to use some Tenderly features with unverified contracts, with limited functionality. For example, you can use the Simulator with raw data. To use the full power of various Tenderly features, it's required to [verify the contracts](../smart-contract-verification/).
{% endhint %}

## Adding a publicly verified contract

To add a verified contract to your project, navigate to the **Contracts** tab in the left sidebar. Once you open the dedicated contract section, click the **Add Contract** button in the top right corner.

![Adding a contract](<../../.gitbook/assets/image1 (1)>)

This will open the Add Contract modal where you need to follow a few steps:

<mark style="color:purple;">**1.**</mark> Enter the address of the contract you wish to add to Tenderly.

<mark style="color:purple;">**2.**</mark> Choose the network to which the contract has been deployed and that Tenderly supports.

<mark style="color:purple;">**3.**</mark> Skip the **This contract is unverified** box since you're adding a verified contract.

![Adding a contract: enter the address and select the network](<../../.gitbook/assets/image4 (1)>)

<mark style="color:purple;">**4.**</mark> Hit the **Add Contract** button and the contract will be added to your project.

<mark style="color:purple;">**5.**</mark> Find and click the added contract from the updated list to open the additional information about it.

![Added contract in the dashboard](../../.gitbook/assets/image7)

## Adding an unverified contract

Follow the same first steps as when adding verified contracts:

<mark style="color:purple;">**1.**</mark> Navigate to the **Contracts** page and click the **Add contract** button.

<mark style="color:purple;">**2.**</mark> Fill in the address and select one of the 20+ networks supported by Tenderly.

<mark style="color:purple;">**3.**</mark> Tick the **This contract is unverified** box.

![Adding an unverified contract](../../.gitbook/assets/image10)



### How to determine if a contract is verified?

If you're uncertain if a contract is verified when adding it, do the following:

* **Check whether a contract is verified on Etherscan or BlockSbcout**. Search for the contract by pasting its address in the search bar or entering its name in the **Verified Contracts** submenu. If the contract is verified, it will have a green checkmark and the "Contract Source Code Verified" label.
* **Search for the contract on Tenderly**. Type in the contract name or address in the Tenderly search bar. If the contract is unverified, it will be displayed only with an address, whereas a verified contract shows a name. Also, if you're uploading a new contract to Tenderly for the first time, it's likely to be unverified.

{% content-ref url="public-contracts.md" %}
[public-contracts.md](public-contracts.md)
{% endcontent-ref %}

{% content-ref url="proxy-contracts.md" %}
[proxy-contracts.md](proxy-contracts.md)
{% endcontent-ref %}

