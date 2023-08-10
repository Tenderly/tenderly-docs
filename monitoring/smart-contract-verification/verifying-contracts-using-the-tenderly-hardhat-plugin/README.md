---
description: >-
  This guide covers contract verification using the Tenderly Hardhat plugin. It
  explores how to verify contracts via code which can be checked into source
  control.
---

# Verifying Contracts Using the Tenderly Hardhat Plugin

When it comes to the Tenderly Hardhat plugin, there are 3 ways to verify your Smart Contracts:

* **Automatic**: The verification happens seamlessly just after the contract is deployed. You don’t have to take any additional steps.
* **Simple manual**: You need to call the verification explicitly (`tenderly.verify()`), which requires you to pass a minimal configuration object: the name and the address.
* **Advanced manual**: You must call the verification explicitly (`tenderly.verifyMultiCompilerAPI()`). This requires you to pass a very detailed configuration object: all the contracts involved, their source, the addresses they’re deployed at, all the libraries used, and Solidity compiler configuration.

{% hint style="success" %}
Whether using automatic or manual approach, verification can happen only after the contract deployment is confirmed. Calling the blocking `deployed` method on the contract:

```
const Ctrct = await ethers.getContractFactory("Ctrct");
const ctrct = await ctrct.deploy();

await ctrct.deployed(); // hardhat-tenderly plugin verifies the contract
// if automatic, the contract is deployed
// if manual, paste the verification code here
```
{% endhint %}

Before starting the process of verification using one of these methods, you need to set up your development environment.

{% hint style="info" %}
You can find a [**demo project on Git**](https://github.com/Tenderly/hardhat-tenderly/tree/master/examples/contract-verification), showing different configuration options and possible ways to verify Smart Contracts.
{% endhint %}

## Setting up the environment

To use a specific Tenderly contract verification method, you need a Hardhat project and a Tenderly API key.

* Start off with an [empty Hardhat project](https://hardhat.org/tutorial/creating-a-new-hardhat-project) and follow along with the guides.
* Alternatively, take a look at the [complete example project on Git](https://github.com/Tenderly/hardhat-tenderly/tree/master/examples/contract-verification).
* Next, authenticate with Tenderly. You can authenticate in two ways:
  * Recommended option: Login using [Tenderly CLI](https://github.com/Tenderly/tenderly-cli#login)

```
tenderly login
```

* Generate an API key in the Dashboard and place it in `~/.tenderly/config.yaml` under `access_key.`

## Installing the Tenderly Hardhat plugin

Once you set up your environment, install the Tenderly plugin for Hardhat:

```bash
npm install --save-dev @tenderly/hardhat-tenderly
```

{% hint style="info" %}
Tenderly Hardhat plugin creates a **deployments** directory where it stores intermediary information about deployments. It's not necessary to keep it in VCS.

```bash
cat >> .gitignore <<EOF

# hardhat-tenderly plugin
deployments
EOF
```
{% endhint %}

After installing the Tenderly package, go to `hardhat.config.js` (or `hardhat.config.ts` if you’re using TypeScript), import the Tenderly Hardhat library and initialize the plugin by calling `setup`.

```tsx
import * as tdly from "@tenderly/hardhat-tenderly";
tdly.setup();
```

Take a look at the [complete Hardhat config file](https://gist.github.com/lucko515/fb36956d56fa56927ab97facae5db6fd).

For now, remember it’s important to call `tenderly.setup()` so the plugin initializes. The plugin is in the automatic verification mode by default. In the case you wish to go for manual verification, pass a configuration argument:

```tsx
tdly.setup({ automaticVerifications: false });
```

Next, you need to extend hardhat configuration with information about the project and your access data:

```
//File:  hardhat.config.ts
//...

const config: HardhatUserConfig = {
  solidity: {...},
  networks: {...},
  tenderly: {
    project: 'my-project-slug',
    username: 'my-username'
  }
```

Replace the `my-project-slug` and `my-username` with appropriate values you can [find in the dashboard](../../../other/platform-access/how-to-find-the-project-slug-username-and-organization-name.md).

## Using an example contract

The following examples use a simple contract automatically generated when you start a new Hardhat project - **Greeter**:

```solidity
//SPDX-License-Identifier: Unlicense
pragma solidity ^0.8.9;

import "hardhat/console.sol";

contract Greeter {
   string private greeting;

   constructor(string memory _greeting) {
       console.log("Deploying a Greeter with greeting:", _greeting);
       greeting = _greeting;
   }

   function greet() public view returns (string memory) {
       return greeting;
   }

   function setGreeting(string memory _greeting) public {
       console.log("Changing greeting from '%s' to '%s'", greeting, _greeting);
       greeting = _greeting;
   }
}
```
