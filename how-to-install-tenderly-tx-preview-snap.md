---
description: >-
  Preview transactions before sending them on-chain to get valuable insights,
  avoid failed transactions, and save funds.
---

# 🦊 Tenderly Tx Preview Snap

{% embed url="https://youtu.be/E8TGyDlV8wQ" %}
Tenderly TX Preview Snap Demo
{% endembed %}

Tenderly TX Preview is a MetaMask Snap that enables you to preview transaction outcomes without actually executing a transaction on a production network. This Snap gives you a human-readable overview of transaction outcomes across [30+ supported EVM networks](https://docs.tenderly.co/supported-networks-and-languages) so you can understand their financial implications before sending them on-chain.

More specifically, Tenderly TX Preview snap shows you which assets will be transferred within your transaction should you decide to send it. It also shows you the corresponding dollar values of asset transfers for ERC-20 and ERC-721 tokens.&#x20;

With Tenderly TX Preview Snap, you can:

* **Get accurate information** on asset transfers with dollar values.
* **Avoid paying gas fees** for reverted transactions and save funds.
* **Send transactions confidently** knowing what’s going to happen.
* **Inspect simulated transactions** in greater detail on Tenderly.
* **Share simulated transactions** publicly with team members or associates.

<figure><img src="https://lh3.googleusercontent.com/kinXDMY5IjfizmpaqEzrGcFenVhDVKSTdEimtaxyZdOyVS3ed_SwXZq4k2AzOwEAotZbm1GEv05J_i6s80YI9jAfXg50nAY_wuHhmDGl8ga96XwtCjwxrEt9Et8rWcJ9FyMKjSB0_gywtcV2YbL8njs" alt=""><figcaption><p>Tenderly TX Preview Snap</p></figcaption></figure>

## What does Tenderly TX Preview Snap do?

Tenderly TX Preview Snap simulates your transactions without sending them on-chain. It sends a request to the [Tenderly Simulation API](https://docs.tenderly.co/simulations-and-forks/simulation-api) and simulates transaction execution against the most recent state of a selected network. It then returns a detailed response on the simulated transaction execution and provides you with a detailed overview of transferred assets.

The Snap also enables you to examine a simulated transaction in greater detail on Tenderly. Simply click the link to the Tenderly Dashboard, where you can find more information on emitted events, state changes, gas consumption, and more.

Finally, transactions simulated using Tenderly TX Preview Snap are publicly sharable. You can share them with your team or associates even if they don’t have a Tenderly account.

## How to install the Tenderly TX Preview Snap?

To install the Tenderly TX Preview Snap, follow these steps:

1. Create a [free Tenderly account](https://dashboard.tenderly.co/register/) or log in if you already have one.
2. [Go to the Authorization page](https://dashboard.tenderly.co/account/authorization) to connect to the Snap.
3. Click the **Connect to Tenderly Snap** button, which will open a pop-up.

<figure><img src="https://lh3.googleusercontent.com/41aXtsb8BnrM8f-CFRBfmW9TyMhF_FqtcHCRVcG0vVGtKL5Jgpzn9t7DbSlj1Lu8p9e0rAebT7xjVfOy5_AFOszdJ84j6GawHZGbRPnA7StMwaxJ0dOKMm01VtwnLmH1LreoJFMmrkjp0lR8FKAFw9w" alt=""><figcaption><p>Authorization page on Tenderly Dashboard</p></figcaption></figure>

4. Select a different project from the drop-down menu and change the access token label. This is an optional step - you can also use the default project and token label.
5. Click the **Connect** button.

<figure><img src="https://lh5.googleusercontent.com/b_MlybtR3kaPi3kPjC_55XgaAqtoJBD7nnTchkgHakfU-E6NTYjHSFgj5epBdcD_3-060GfAh2RFmYjbFAdbmK_kxHRKaueUqSOKkY2MC8cJtuD4eBqrcuDL22KpyDSPu3VVvXlfgFoYIBPHwedITWc" alt=""><figcaption><p>Connect to Tenderly Snap instructions</p></figcaption></figure>

This automatically installs Tenderly TX Preview Snap and sets up your credentials within your MetaMask wallet so you don’t have to do this manually.

## What does the Tenderly TX Preview Snap NOT do?

Tenderly TX Preview Snap **does not execute** your transactions on-chain. All transactions are simulated against the most recent state of a selected network using the Tenderly Simulation API.

## What networks does Tenderly TX Preview Snap support?

Tenderly TX Preview Snap supports more than 30 EVM-compatible networks. The list includes major chains such as Ethereum Mainnet and its testnets, Optimism, Arbitrum, Base, and Polygon. Check out the [complete list of supported networks on Tenderly](https://docs.tenderly.co/supported-networks-and-languages).&#x20;

This means that you can simulate transaction execution against any of the networks from the list provided that it’s supported by the dapp or wallet you’re using.

## How to use the Tenderly TX Preview Snap?

After installing the Tenderly TX Preview Snap, you can start using it right away. Just connect to the dapp you typically use and continue using MetaMask as usual. Once you initiate a transaction, you’ll notice an additional tab where you find transaction simulation insights.

## Where can I find simulated transactions?

All simulated transactions are saved within the project created for the account you used to install the Snap. You can find them in the list of simulated transactions on the Simulator page.

For example, if you use an account named “Bob” and create a project “mm-snap”, you can find your simulated transactions on this URL: [https://dashboard.tenderly.co/bob/mm-snap/simulator](https://dashboard.tenderly.co/bob/mm-snap/simulator).

## How do I reach out for snap support?

If you have any questions or come across any issues while installing or using the Tenderly TX Preview Snap, feel free to reach out to us at [metamask.snap@tenderly.co](mailto:metamask.snap@tenderly.co).
