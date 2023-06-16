---
description: >-
  Learn how to use and access token data, including dollar value changes, from
  the asset_changes object returned by the Simulation API and Transaction Trace
  endpoints.
---

# Asset Changes

{% embed url="https://github.com/Tenderly/tenderly-metamask-snap-simulate-asset-changes" %}
Tenderly MetaMask Snap using the Tenderly Simulation API to showcase transaction asset changes
{% endembed %}

`asset_changes` is an object that is returned as part of the response from the Simulation API and Transaction Trace. This object contains information about the token, including the token's dollar value.&#x20;

The conversion from tokens to dollars is processed by Tenderly in real time using the most accurate market data. This eliminates the need for you to use additional tools or rely on third-party integrations to facilitate the conversion from tokens to dollars.&#x20;

For wallets, DeFi projects, and DEXs, displaying the token's dollar value to users within simulations makes the transaction more human-readable. This can also help users better understand the impact of their transactions before making a commitment.

The most commonly used token standards are supported: **ERC20** and **ERC721**.

The displayed dollar value represents the **current dollar value** -- not historical.

### `asset_changes` object

{% hint style="info" %}
You need a Tenderly account to use the Transaction Trace and Simulation APIs. [Create a free Tenderly account here](https://dashboard.tenderly.co/register).
{% endhint %}

Once logged in and authenticated, you can call the following API URLs:

**Simulation API** ([Learn more](simulation-api/))

```
https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/simulate
```

**Transaction Trace API**

```
https://api.tenderly.co/api/v1/public-contract/:networkId/trace/:txHash 
```

The `asset_changes` object is accessible through `transaction` > `transaction_info` > `asset_changes` within the response from the Transaction Trace and Simulation API.

The object contains the following array of data detailing the asset changes that have occurred.

* **`asset_changes`** (array)
  * **`type`** (string): Can be transfer, mint, burn
  * **`from`** (string): Address of the sender (Empty for mint transfers)
  * **`to`** (string): Address of the receiver (Empty for burn transfers)
  * **`amount`** (string): The amount of the token that was transferred
  * **`raw_amount`** (string): Raw amount transfer for the token
  * **`dollar_value`**(string): Dollar value of the transferred token
  * **`token_info`**(object):
    * **`standard`** (string): Supported token standards: ERC20, ERC721, NativeCurrency
    * **`type`** (string): The token type: Native, Fungible, Non-Fungible
    * **`contract_address`**(string) : Address of the contract
    * **`symbol`** (string): Token symbol
    * **`name`** (string): Token name
    * **`logo`** (string): URL for the token icon
    * **`decimals`** (int): Number of decimals in the token
    * **`dollar_value`**(string): Dollar value of a single ERC20 token
