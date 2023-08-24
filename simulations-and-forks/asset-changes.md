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

{% tabs %}
{% tab title="ERC20 Swap Example" %}
```json
[
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
      "symbol": "weth",
      "name": "WETH",
      "logo": "https://assets.coingecko.com/coins/images/2518/large/weth.png?1628852295",
      "decimals": 18,
      "dollar_value": "1677.3499755859375"
    },
    "type": "Mint",
    "to": "0x3fc91a3afd70395cd496c647d5a6cc9d4b2b7fad",
    "amount": "0.004",
    "raw_amount": "4000000000000000",
    "dollar_value": "6.7093999023437499996"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
      "symbol": "weth",
      "name": "WETH",
      "logo": "https://assets.coingecko.com/coins/images/2518/large/weth.png?1628852295",
      "decimals": 18,
      "dollar_value": "1677.3499755859375"
    },
    "type": "Transfer",
    "from": "0x3fc91a3afd70395cd496c647d5a6cc9d4b2b7fad",
    "to": "0xdfc14d2af169b0d36c4eff567ada9b2e0cae044f",
    "amount": "0.004",
    "raw_amount": "4000000000000000",
    "dollar_value": "6.7093999023437499996"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0x7fc66500c84a76ad7e9c93437bfc5ac33e2ddae9",
      "symbol": "aave",
      "name": "Aave",
      "logo": "https://assets.coingecko.com/coins/images/12645/large/AAVE.png?1601374110",
      "decimals": 18,
      "dollar_value": "57.09000015258789"
    },
    "type": "Transfer",
    "from": "0xdfc14d2af169b0d36c4eff567ada9b2e0cae044f",
    "to": "0xe8e6959a29bb94cb1080de4257417e6f22ab3ae2",
    "amount": "0.114329491204601088",
    "raw_amount": "114329491204601088",
    "dollar_value": "6.527070670315972013"
  },
  {
    "token_info": {
      "standard": "NativeCurrency",
      "type": "Native",
      "symbol": "eth",
      "name": "Ethereum",
      "logo": "https://assets.coingecko.com/coins/images/279/large/ethereum.png?1595348880",
      "decimals": 18,
      "dollar_value": "1677.5799560546875"
    },
    "type": "Transfer",
    "from": "0xe8e6959a29bb94cb1080de4257417e6f22ab3ae2",
    "to": "0x3fc91a3afd70395cd496c647d5a6cc9d4b2b7fad",
    "amount": "0.004",
    "raw_amount": "4000000000000000",
    "dollar_value": "6.7103198242187499997"
  },
  {
    "token_info": {
      "standard": "NativeCurrency",
      "type": "Native",
      "symbol": "eth",
      "name": "Ethereum",
      "logo": "https://assets.coingecko.com/coins/images/279/large/ethereum.png?1595348880",
      "decimals": 18,
      "dollar_value": "1677.5799560546875"
    },
    "type": "Transfer",
    "from": "0x3fc91a3afd70395cd496c647d5a6cc9d4b2b7fad",
    "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
    "amount": "0.004",
    "raw_amount": "4000000000000000",
    "dollar_value": "6.7103198242187499997"
  }
]
```
{% endtab %}

{% tab title="NFT Transfer Example" %}
```json
[
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Mint",
    "to": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "amount": "9.434",
    "raw_amount": "9434000000000000000",
    "dollar_value": "97.45321928024291992"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Transfer",
    "from": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "to": "0x64c4607ad853999ee5042ba8377bfc4099c273de",
    "amount": "0.075",
    "raw_amount": "75000000000000000",
    "dollar_value": "0.7747499942779541016"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Transfer",
    "from": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "to": "0x2fffffb80ea0c59ca19258872351ae4a43facb37",
    "amount": "0.18",
    "raw_amount": "180000000000000000",
    "dollar_value": "1.8593999862670898438"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Transfer",
    "from": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "to": "0xd7b87018c0434427f3a1f9d8c26c3f1a8a759b1b",
    "amount": "2.745",
    "raw_amount": "2745000000000000000",
    "dollar_value": "28.355849790573120116"
  },
  {
    "token_info": {
      "standard": "ERC721",
      "type": "NonFungible",
      "contract_address": "0x7a420aeff902aaa2c85a190d7b91ce8beffffe14",
      "symbol": "DCGHERO",
      "name": "Dragon Crypto Hero",
      "logo": "https://assets.coingecko.com/nft_contracts/images/1461/small/dragon-crypto-hero.png?1662020122",
      "decimals": 0,
      "dollar_value": "28.489999771118164"
    },
    "type": "Transfer",
    "from": "0xd7b87018c0434427f3a1f9d8c26c3f1a8a759b1b",
    "to": "0xe8e6959a29bb94cb1080de4257417e6f22ab3ae2",
    "amount": "1",
    "raw_amount": "1",
    "token_id": "0x0000000000000000000000000000000000000000000000000000000000000489",
    "dollar_value": "28.489999771118164062"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Transfer",
    "from": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "to": "0x64c4607ad853999ee5042ba8377bfc4099c273de",
    "amount": "0.075",
    "raw_amount": "75000000000000000",
    "dollar_value": "0.7747499942779541016"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Transfer",
    "from": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "to": "0xb090fc5d0c06804dfbf06efb59ce1f291f13162a",
    "amount": "0.15",
    "raw_amount": "150000000000000000",
    "dollar_value": "1.5494999885559082032"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Transfer",
    "from": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "to": "0x2ce84ba90f3cd2c9281cc3170295d84b60ac28b4",
    "amount": "2.775",
    "raw_amount": "2775000000000000000",
    "dollar_value": "28.66574978828430176"
  },
  {
    "token_info": {
      "standard": "ERC721",
      "type": "NonFungible",
      "contract_address": "0xb42d0f524564cafe2a47ca3331221903eda83b3c",
      "symbol": "MONKEEZ",
      "name": "Monkeez",
      "logo": "https://assets.coingecko.com/nft_contracts/images/1417/small/monkeez.png?1662019843",
      "decimals": 0,
      "dollar_value": "25.670000076293945"
    },
    "type": "Transfer",
    "from": "0x2ce84ba90f3cd2c9281cc3170295d84b60ac28b4",
    "to": "0xe8e6959a29bb94cb1080de4257417e6f22ab3ae2",
    "amount": "1",
    "raw_amount": "1",
    "token_id": "0x0000000000000000000000000000000000000000000000000000000000000190",
    "dollar_value": "25.670000076293945312"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Transfer",
    "from": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "to": "0x64c4607ad853999ee5042ba8377bfc4099c273de",
    "amount": "0.02475",
    "raw_amount": "24750000000000000",
    "dollar_value": "0.25566749811172485352"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Transfer",
    "from": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "to": "0x5b34932f643a143bdc9801064ea06526ba9476af",
    "amount": "0.0495",
    "raw_amount": "49500000000000000",
    "dollar_value": "0.51133499622344970705"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Transfer",
    "from": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "to": "0x9aa4b22a616d5cbc6834d3e5da877d17f93c2b77",
    "amount": "0.91575",
    "raw_amount": "915750000000000000",
    "dollar_value": "9.45969743013381958"
  },
  {
    "token_info": {
      "standard": "ERC721",
      "type": "NonFungible",
      "contract_address": "0x4245a1bd84eb5f3ebc115c2edf57e50667f98b0b",
      "symbol": "HOP",
      "name": "Hoppers Game",
      "logo": "https://assets.coingecko.com/nft_contracts/images/1448/small/hoppers-game.png?1662020093",
      "decimals": 0,
      "dollar_value": "8.229999542236328"
    },
    "type": "Transfer",
    "from": "0x9aa4b22a616d5cbc6834d3e5da877d17f93c2b77",
    "to": "0xe8e6959a29bb94cb1080de4257417e6f22ab3ae2",
    "amount": "1",
    "raw_amount": "1",
    "token_id": "0x00000000000000000000000000000000000000000000000000000000000011eb",
    "dollar_value": "8.229999542236328125"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Transfer",
    "from": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "to": "0x64c4607ad853999ee5042ba8377bfc4099c273de",
    "amount": "0.0611",
    "raw_amount": "61100000000000000",
    "dollar_value": "0.63116299533843994143"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Transfer",
    "from": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "to": "0xcafbcfd3fe93bccf1e15fa831f7d98ecfab4e281",
    "amount": "0.1222",
    "raw_amount": "122200000000000000",
    "dollar_value": "1.2623259906768798829"
  },
  {
    "token_info": {
      "standard": "ERC20",
      "type": "Fungible",
      "contract_address": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
      "symbol": "wavax",
      "name": "Wrapped AVAX",
      "logo": "https://assets.coingecko.com/coins/images/15075/large/wrapped-avax.png?1629873618",
      "decimals": 18,
      "dollar_value": "10.329999923706055"
    },
    "type": "Transfer",
    "from": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "to": "0xaee1806aefbe8068db299c4c859937a1aee55dae",
    "amount": "2.2607",
    "raw_amount": "2260700000000000000",
    "dollar_value": "23.353030827522277832"
  },
  {
    "token_info": {
      "standard": "ERC721",
      "type": "NonFungible",
      "contract_address": "0x3025c5c2aa6eb7364555aac0074292195701bbd6",
      "symbol": "MADSKULLZ",
      "name": "MadSkullz",
      "logo": "https://assets.coingecko.com/nft_contracts/images/1407/small/madskullz.png?1662019779",
      "decimals": 0,
      "dollar_value": "29.829999923706055"
    },
    "type": "Transfer",
    "from": "0xaee1806aefbe8068db299c4c859937a1aee55dae",
    "to": "0xe8e6959a29bb94cb1080de4257417e6f22ab3ae2",
    "amount": "1",
    "raw_amount": "1",
    "token_id": "0x0000000000000000000000000000000000000000000000000000000000000827",
    "dollar_value": "29.829999923706054688"
  },
  {
    "token_info": {
      "standard": "NativeCurrency",
      "type": "Native",
      "symbol": "avax",
      "name": "Avalanche",
      "logo": "https://assets.coingecko.com/coins/images/12559/large/Avalanche_Circle_RedWhite_Trans.png?1670992574",
      "decimals": 18,
      "dollar_value": "10.210000038146973"
    },
    "type": "Transfer",
    "from": "0xe8e6959a29bb94cb1080de4257417e6f22ab3ae2",
    "to": "0xae079eda901f7727d0715aff8f82ba8295719977",
    "amount": "9.434",
    "raw_amount": "9434000000000000000",
    "dollar_value": "96.32114035987854004"
  },
  {
    "token_info": {
      "standard": "NativeCurrency",
      "type": "Native",
      "symbol": "avax",
      "name": "Avalanche",
      "logo": "https://assets.coingecko.com/coins/images/12559/large/Avalanche_Circle_RedWhite_Trans.png?1670992574",
      "decimals": 18,
      "dollar_value": "10.210000038146973"
    },
    "type": "Transfer",
    "from": "0xbb01d7ad46a1229f8383f4e863abf4461b427745",
    "to": "0xb31f66aa3c1e785363f0875a1b74e27b85fd66c7",
    "amount": "9.434",
    "raw_amount": "9434000000000000000",
    "dollar_value": "96.32114035987854004"
  }
]
```
{% endtab %}
{% endtabs %}
