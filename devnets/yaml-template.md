---
description: Use the built-in YAML editor to define a DevNet template using YAML.
---

# YAML Template

DevNet templates can be defined using YAML. These YAML templates are reusable, enabling you to quickly spawn highly customized DevNet environments.

{% hint style="info" %}
DevNet templates cannot be modified once they have been saved.
{% endhint %}

YAML DevNet templates have one mandatory and multiple optional fields.

The mandatory field `template` is where you specify basic information about the template and the network fork configurations.

The following optional fields can be used to override on-chain data with custom values: `wallets`, `contracts`, `storage`, `balances`, and `erc20`.

### Create a DevNet template in YAML

1. Log into your Tenderly account.
2. [Navigate to the **DevNets**](https://dashboard.tenderly.co/register?redirectTo=devnets) section and click **Create Template**.
3. Use the YAML editor to define your DevNet template.

<figure><img src="../.gitbook/assets/yaml template.png" alt=""><figcaption><p>Create DevNet YAML template</p></figcaption></figure>

### Mandatory fields

#### Template

The mandatory template field must contain the following key-value pairs:

```yaml
template:
  name: # Your template's unique name
  block-number: # Desired block number (e.g., latest or 123456)
  visibility: # Scope of visibility (TEAM or PERSONAL)
  network-id: # Network ID number (e.g., 1 for the Ethereum Mainnet)
  execution:
    chain-config:
      chain-id: # Network chain ID (e.g., 1 for Ethereum)
    block-gas-limit: # Maximum amount of gas in Wei (e.g., 10000000)
    base-fee-per-gas: # Base fee per gas in Wei (e.g., 1000000000)
```

The network name or ID, block number, template name, and visibility are pulled from the UI form automatically. However, they can be manually adjusted in the YAML editor.

### Optional fields

#### **Contracts**

Add the `contracts` field to override the on-chain data of a specific contract with custom values. You can modify the balance on the contracts as well as storage variables.

```yaml
contracts:
    - address: # contract address
      bytecode: # contract bytecode
      nonce: # 0
      balance: # custom balance
      slots: # format: slot address: value
        - 0x34590...988c: # value
        - 0x34590...c88d: # value
```

#### **Wallets**

Add the `wallets` field to modify the balance on a specific wallet. You need to provide the wallet address and specify the desired balance for that wallet to have on your DevNet.

```yaml

  wallets:
    - address: # wallet address
      nonce: # 0 
      balance: # custom balance

```

#### **Storage**

Add the `storage` field to override storage variables for contracts and wallets. The `address` field can be a contract or wallet address. You can include multiple address fields following the format below.

```yaml

  storage:
    - address: # contract or wallet address
      slots: # format: slot address: value
        - 0x1459...3988c: # value
        - 0x2459...3988c: #value
```

#### **Balances**

Add the `balances` field to override the balance on a contract or a wallet. You can include multiple `address` fields at once.

```yaml

  balances:
    - address: # contract or wallet address
      amount: # custom balance
```

#### **ERC-20**

Add the `erc20` field to change the balances of addresses for specific ERC-20 contracts. You can modify the balances on multiple ERC-20 contracts as well as multiple addresses within each contract at once, following the format below.

```yaml

  erc20:
    - contract: # ERC-20 token contract address
      balances:
        - address: # wallet or contract address
          amount: 100
```

### **Validating the YAML template**

Ensure the syntax is correct by using the built-in YAML validation tool on the Tenderly Dashboard. After successful validation, click on **Create** to save your template. The newly created template will now be listed under the available templates on the DevNets page.

You can use this template to spawn a DevNet environment that reflects the configurations you’ve defined in the YAML file.
