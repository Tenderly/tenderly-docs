---
description: >-
  Learn more about the Transaction Preview feature for wallets and how to
  integrate it using the Tenderly Simulation Infrastructure.
---

# Transaction Preview

## Introduction

Transaction Preview is an implementation of the [Tenderly Simulation Infrastructure](intro-to-simulations.md) in wallets. It allows users to simulate individual or chained transactions and preview their execution without sending them on-chain.&#x20;

By previewing exact transaction outcomes, wallet users can avoid failed transactions, unnecessary gas costs, and hidden security risks. They also receive detailed, human-readable information about transaction simulations. This way, users get a better overall experience and increased security when using wallets.

Additionally, since Tenderly supports all [major EVM-compatible chains](https://docs.tenderly.co/supported-networks-and-languages), the Tenderly Simulation Infrastructure offers reliable results in a multi-chain environment. This also enables wallet users to switch between different networks seamlessly.&#x20;

## Use Cases

To add Transaction Preview to your wallet, you need to integrate the [Tenderly Simulation API](https://docs.tenderly.co/simulations-and-forks/simulation-api). This way, you can reduce the number of failed transactions and improve your users' experience in multiple ways.&#x20;

### Prevent unnecessary spending

By allowing users to dry-run transactions, you help them avoid paying gas fees for reverted transactions. You can also provide accurate gas estimates across multiple networks, ensuring they don't underpay or overpay for gas.&#x20;

Additionally, you can display human-readable warnings against transaction failures caused by other types of issues other than insufficient gas. This way, you can save valuable resources and minimize the number of failed transactions in your wallet.&#x20;

### Enable informed decision making

Enable your users to make informed and confident decisions when sending transactions on-chain. Help them understand the financial implications of their transactions with greater visibility and predictability into their outcomes.&#x20;

You can achieve this by displaying:&#x20;

* **Asset changes:** Show all token transfers, including fungible, non-fungible, and native tokens, with their exact dollar values.
* **Balance changes:** Give an aggregated view of asset changes per address, with the corresponding dollar amount adjustments.
* **Fully decoded logs:** Provide decoded information about emitted events, log names, and related parameters for comprehensive insights into transaction execution.&#x20;

### Secure the execution of complex, chained transactions

Allow your users to simulate an array of transactions with [Simulation Bundles](simulation-api/simulation-bundles.md). Then, display results for each step and help them:

* **Validate transaction workflows on DeFi platforms** when executing and approving swaps that entail multiple intermediate steps. This can prevent potential mistakes or unintended consequences before submitting transactions on-chain.&#x20;
* **Identify security risks** and/or vulnerabilities by surfacing all smart contracts a transaction interacts with.&#x20;
* **Validate the NFT minting and trading process**, including token metadata handling and associated fees. This ensures that NFT minting and trading are seamless for users and minimizes risks related to incorrect data or token ownership.

## Practical examples

Follow the step-by-step guides below to learn how to implement Transaction Preview into example wallets.&#x20;

### Add Transaction Preview to a MetaMask Snap

Integrate Transaction Preview into a [MetaMask Snap](https://metamask.io/snaps/) wallet using the Tenderly Simulation API. Enable users to preview the exact outcomes of ERC-20 and ERC-721 transactions. Show detailed information about asset changes with dollar values, native-asset balance changes, output values, storage changes, event logs, and call traces.

Watch the example overview video:

{% embed url="https://youtu.be/DgfTifOM_V0" %}
Tenderly MetaMask Snap Demo
{% endembed %}

See the open-source GitHub repository here:

{% embed url="https://github.com/Tenderly/tenderly-metamask-snap-simulate-asset-changes" %}
See an open-source implementation of the Tenderly Snap
{% endembed %}

Follow a step-by-step tutorial to learn how to connect the Tenderly Simulation API, send transaction data, retrieve simulation results, and display them to the user via the MetaMask Snap UI.&#x20;

{% content-ref url="integration-guides/how-to-add-transaction-preview-to-a-metamask-snap-using-tenderly-simulation-api.md" %}
[how-to-add-transaction-preview-to-a-metamask-snap-using-tenderly-simulation-api.md](integration-guides/how-to-add-transaction-preview-to-a-metamask-snap-using-tenderly-simulation-api.md)
{% endcontent-ref %}

#### Examples

<figure><img src="../.gitbook/assets/image (106).png" alt=""><figcaption><p>A successful ERC20 token transfer of 1 USDC to demo.eth</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (107).png" alt=""><figcaption><p>A successful ERC721 (NFT) token transfer of 1 Crypto Bull to other address.</p></figcaption></figure>

### Add Transaction Preview to a Rabby Wallet

Integrate the Tenderly Simulation API into an [open-source Rabby Wallet example](https://github.com/RabbyHub/Rabby) to enable Transaction Preview.&#x20;

See the preview of an ERC-20 transaction in this video:

{% embed url="https://youtu.be/6Dqd_1EANfY" %}
Transaction Preview in Rabby Wallet for ERC20 Token Transfers
{% endembed %}

Watch the example with an ERC-721 transaction preview:&#x20;

{% embed url="https://youtu.be/uLt9r4ATLy8" %}
Transaction Preview in Rabby Wallet for NFT Token Transfers
{% endembed %}

Find an open-source GitHub repository here:

{% embed url="https://github.com/Tenderly/tenderly-rabby-transaction-preview" %}
See an open-source implementation of the Tenderly Rabby Transaction Preview
{% endembed %}

#### Examples

<figure><img src="../.gitbook/assets/image (108).png" alt=""><figcaption><p>Transaction Preview in Rabby Wallet on Uniswap ERC20 Swap Example</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (109).png" alt=""><figcaption><p>Transaction Preview in Rabby Wallet on Joepegs NFT Example</p></figcaption></figure>

## Resources

To learn more about the Tenderly Simulation API, check out these helpful links:

* [Simulation API ](simulation-api/)
* [Asset Changes](asset-changes.md)&#x20;
* [Simulation Bundles](simulation-api/simulation-bundles.md)&#x20;
