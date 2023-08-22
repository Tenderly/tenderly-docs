---
description: >-
  Learn how to verify proxy contracts on Tenderly using the Tenderly Hardhat
  plugin.
---

# Verifying Proxy Contracts on Tenderly

To get full support for transactions debugging, monitoring, and alerting with proxy contracts, you need to verify the following:

* Proxy contract
* Implementation behind the proxy
* Any dependencies the implementation has
* New implementation instances deployed with upgrades

<figure><img src="../../../.gitbook/assets/image (104).png" alt=""><figcaption></figcaption></figure>

The verification process varies depending on the proxy contract type and approach to the implementation.

### Overview

In this guide, we'll use [an example Hardhat project](https://github.com/Tenderly/tenderly-examples) and the `@tenderly/tenderly-hardhat` plugin to demonstrate the verification of OpenZeppelin's [UUPSUpgradeable](https://docs.openzeppelin.com/contracts/4.x/api/proxy#UUPSUpgradeable), [TransparentUpgradeableProxy](https://docs.openzeppelin.com/contracts/4.x/api/proxy#TransparentUpgradeableProxy), and [BeaconProxy](https://docs.openzeppelin.com/contracts/4.x/api/proxy#BeaconProxy) alternatives.

{% hint style="warning" %}
Proxy contracts need to be [verified manually](manual-contract-verification.md). Turn off automatic verification like so:

```typescript
import * as tenderly from "@tenderly/hardhat-tenderly";
// use manual verification
tenderly.setup({ automaticVerifications: false });
```
{% endhint %}

To obtain the address of the deployed implementation, use the `@openzeppelin/upgrades-core` package.

Verifying the proxy implementation is usually straightforward; verify it just like any other contract:

```ts
await tenderly.verify({
  // the new implementation contract
  name: "VaultV2",
  // the address where implementation is deployed
  address: await getImplementationAddress(ethers.provider, proxy.address),
});
```

To verify the proxy instance, you need to complete these two preliminary steps:

* [Load the exact smart contract of the proxy](verifying-proxy-contracts-on-tenderly.md#loading-proxy-contracts) so it gets compiled, depending on the type of proxy you're using. To make this happen, you'll need to put the proxy contracts through the compiler by creating a dummy proxy file.
* [Modify `hardhat.config.ts`](verifying-proxy-contracts-on-tenderly.md#configuring-solidity-compiler-overrides) to match the settings used to compile OpenZeppelin contracts.

Once these steps are completed, you can proceed to verify the proxy just as you would with any other contract:

```ts
await tenderly.verify({
  name: "ERC1967Proxy", // or TransparentUpgradeableProxy or BeaconProxy
  address: proxy.address,
});
```

### Running the sample

**Step 1:** Clone the repo and install dependencies:

```sh
git clone git@github.com:Tenderly/tenderly-examples.git
cd contract-verification
npm i
```

**Step 2:** Set up the [Tenderly CLI](https://github.com/Tenderly/tenderly-cli):

```sh
brew tap tenderly/tenderly && brew install tenderly
tenderly login
```

**Step 3:** Modify your `hardhat.config.ts` file and update the `tenderly.username` and `tenderly.project` with your Tenderly [username and project slug](../../../other/platform-access/how-to-find-the-project-slug-username-and-organization-name.md).

**Step 4:** The fastest way to deploy and verify contracts is to use [Tenderly DevNets](broken-reference). Log into the [Tenderly Dashboard](https://dashboard.tenderly.co/register?redirectTo=devnets) and create a new DevNet template.&#x20;

<figure><img src="../../../.gitbook/assets/DevNetScreen.png" alt=""><figcaption><p>Project and DevNet slug</p></figcaption></figure>

**Step 5:** Spawn a DevNet from the template you created and use the generated RPC URL. You can spawn a DevNet and obtain the RPC in three ways:

* **Option 1**: Click "Spawn DevNet" from the Dashboard and add the RPC link to `networks.tenderly.url` in the `hardhat.config.ts` file.
* **Option 2**: Run the DevNet spawning command you copied from the Dashboard and paste the RPC link to `networks.tenderly.url` in `hardhat.config.ts` file.
* **Option 3**: Run the `spawn-devnet-to-hardhat` script from the example project, which will spin up a fresh DevNet and update your Hardhat project automatically. Replace `PROJECT_SLUG` and `DEVNET_TEMPLATE_SLUG` with appropriate values. (see the screenshot)

```bash
npm run spawn-devnet-to-hardhat <PROJECT_SLUG> <DEVNET_TEMPLATE_SLUG>
```

**Step 6**: Finally, run the tests:

```sh
rm -rf .openzeppelin &&  npx hardhat test --network tenderly      
```

### Loading proxy contracts

To verify the proxy contract, create a `DummyProxy.sol` file and import the OpenZepplin proxy contracts you're working with. In doing so, these contracts are loaded and have passed through the compiler, enabling you to reference the exact contract source of the proxy during verification.

{% code fullWidth="false" %}
```sol
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.17;

import "@openzeppelin/contracts/proxy/ERC1967/ERC1967Proxy.sol";
import "@openzeppelin/contracts/proxy/beacon/UpgradeableBeacon.sol";
import "@openzeppelin/contracts/proxy/beacon/BeaconProxy.sol";
import "@openzeppelin/contracts/proxy/transparent/TransparentUpgradeableProxy.sol";

abstract contract ERC1967ProxyAccess is ERC1967Proxy {}
abstract contract UpgradableBeaconAccess is UpgradeableBeacon {}
abstract contract BeaconProxyAccess is BeaconProxy {}
abstract contract TransparentUpgradeableProxyAccess is TransparentUpgradeableProxy {}
```
{% endcode %}

### Configuring Solidity compiler overrides

After compiling Openzepplin's proxy contracts, you also need to specify the following:

* Version of the Solidity compiler that was used to compile the contracts
* Optimization settings used by Openzepplin's upgrades plugin when performing proxy deployment/upgrades

{% hint style="info" %}
The `hardhat-tenderly` plugin uses both the source code of smart contracts and compiler settings for verification. If either of these settings is incorrect, the verification will fail.
{% endhint %}

Add the following `overrides` map to the `config.solidity` section of your Hardhat config object:

```ts
const config: HardhatUserConfig = {
  solidity: {
    compilers: [{ version: "0.8.18" } /* OTHER COMPILER VERSIONS*/],
    overrides: {
      "@openzeppelin/contracts/proxy/ERC1967/ERC1967Proxy.sol": {
        version: "0.8.9",
        settings: {
          optimizer: {
            enabled: true,
            runs: 200,
          },
        },
      },
      "@openzeppelin/contracts/proxy/transparent/TransparentUpgradeableProxy.sol":
        {
          version: "0.8.9",
          settings: {
            optimizer: {
              enabled: true,
              runs: 200,
            },
          },
        },

      "@openzeppelin/contracts/proxy/beacon/UpgradeableBeacon.sol": {
        version: "0.8.9",
        settings: {
          optimizer: {
            enabled: true,
            runs: 200,
          },
        },
      },
      "@openzeppelin/contracts/proxy/beacon/BeaconProxy.sol": {
        version: "0.8.9",
        settings: {
          optimizer: {
            enabled: true,
            runs: 200,
          },
        },
      },
      "contracts/proxy.sol": {
        version: "0.8.9",
        settings: {
          optimizer: {
            enabled: true,
            runs: 200,
          },
        },
      },
    },
  },
  /* OTHER CONFIG */
};
```

### Example: Proxied vault

Below are code samples showing the verification of a proxied Vault contract. The Vault references an ERC-20 token (TToken). We'll demonstrate how to verify both the implementation and the proxy using OpenZeppelin's UUPS, Transparent, and Beacon proxying methods.

### Verifying a UUPS proxy

To verify the UUPS proxy and the underlying information, call the `hardhat-tenderly` plugin twice:

1. To verify the implementation, you need to provide the following:
   * `name` of your proxied contract (in our case `Vault`)
   * Address where the contract was deployed using the `getImplementationAddress` method from `@openzeppelin/upgrades-core`.
2. To verify the proxy, provide the following:
   * `ERC1967Proxy` as the proxy contract `name`
   * Address of the proxy `proxy.address`

```ts
await tenderly.verify(
  {
    name: "Vault",
    address: await getImplementationAddress(ethers.provider, proxy.address),
  },
  {
    name: "ERC1967Proxy",
    address: proxy.address,
  }
);
```

#### Complete code sample

Here's a complete Hardhat test that does the following:

* Deploys the `TToken` (needed for the vault)
* Deploys `Vault` as a proxy, initialized with the `TToken` contract
* Verifies the proxy (`ERC1967Proxy`) instance deployed at `proxy.address`
* Verifies the implementation instance `Vault`, deployed at `getImplementationAddress(ethers.provider, proxy.address)`
* Upgrades the proxy to `VaultV2`

```ts
import { getImplementationAddress } from "@openzeppelin/upgrades-core";
import { ethers, tenderly, upgrades } from "hardhat";
import { Vault } from "../typechain-types";

describe("Vault", () => {
  it("uups proxy deployment and verification", async () => {
    const VaultFactory = await ethers.getContractFactory("Vault");
    const TokenFactory = await ethers.getContractFactory("TToken");

    const token = await TokenFactory.deploy();
    await token.deployed();

    await tenderly.verify({
      name: "TToken",
      address: token.address,
    });

    let proxy = await upgrades.deployProxy(VaultFactory, [token.address], {
      kind: "uups",
    });
    await proxy.deployed();

    console.log("Deployed UUPS ", {
      proxy: proxy.address,
      implementation: await getImplementationAddress(
        ethers.provider,
        proxy.address
      ),
    });

    await tenderly.verify(
      {
        name: "Vault",
        address: await getImplementationAddress(ethers.provider, proxy.address),
      },
      {
        name: "ERC1967Proxy",
        address: proxy.address,
      }
    );

    console.log(`Vault version before upgrade: ${await proxy.version()}`);

    // upgrade
    const vaultV2Factory = await ethers.getContractFactory("VaultV2");
    proxy = (await upgrades.upgradeProxy(proxy, vaultV2Factory, {
      kind: "uups",
    })) as Vault;

    await proxy.deployed();

    console.log("Upgraded UUPS ", {
      proxy: proxy.address,
      implementation: await getImplementationAddress(
        ethers.provider,
        proxy.address
      ),
    });

    await tenderly.verify({
      name: "VaultV2",
      address: await getImplementationAddress(ethers.provider, proxy.address),
    });

    console.log(`Vault version after upgrade: ${await proxy.version()}`);
  });
});
```

### Verifying a Transparent proxy

To verify the UUPS proxy and the underlying information, call `hardhat-tenderly` while passing two contracts: `Vault` for the implementation, and `TransparentUpgradeableProxy` for the proxy itself:

```ts
await tenderly.verify(
  {
    name: "Vault",
    address: await getImplementationAddress(ethers.provider, proxy.address),
  },
  {
    name: "TransparentUpgradeableProxy",
    address: proxy.address,
  }
);
```

1. To verify the implementation, provide the following:
   * `name` of your proxied contract (in our case `Vault`)
   * Address where the contract was deployed, using the `getImplementationAddress` method from `@openzeppelin/upgrades-core`.
2. To verify the proxy, provide the following:
   * `TransparentUpgradeableProxy` as the proxy contract `name`
   * Address of the proxy `proxy.address`

#### Complete code sample

```ts
import { getImplementationAddress } from "@openzeppelin/upgrades-core";
import { ethers, tenderly, upgrades } from "hardhat";
import { Vault } from "../typechain-types";

describe("Vault", () => {
  it("transparent upgradable proxy deployment and verification", async () => {
    const VaultFactory = await ethers.getContractFactory("Vault");
    const TokenFactory = await ethers.getContractFactory("TToken");

    const token = await TokenFactory.deploy();
    await token.deployed();

    await tenderly.verify({
      name: "TToken",
      address: token.address,
    });

    let proxy = await upgrades.deployProxy(VaultFactory, [token.address], {
      kind: "transparent",
    });
    await proxy.deployed();

    console.log("Deployed transparent", {
      proxy: proxy.address,
      implementation: await getImplementationAddress(
        ethers.provider,
        proxy.address
      ),
    });

    await tenderly.verify(
      {
        name: "Vault",
        address: await getImplementationAddress(ethers.provider, proxy.address),
      },
      {
        name: "TransparentUpgradeableProxy",
        address: proxy.address,
      }
    );

    console.log(`Vault version before upgrade: ${await proxy.version()}`);

    // upgrade
    const vaultV2Factory = await ethers.getContractFactory("VaultV2");

    proxy = (await upgrades.upgradeProxy(proxy, vaultV2Factory, {
      kind: "transparent",
    })) as Vault;

    await proxy.deployed();

    console.log("Upgraded transparent ", {
      proxy: proxy.address,
      implementation: await getImplementationAddress(
        ethers.provider,
        proxy.address
      ),
    });

    await tenderly.verify({
      name: "VaultV2",
      address: await getImplementationAddress(ethers.provider, proxy.address),
    });

    console.log(`Vault version after upgrade: ${await proxy.version()}`);
  });
});
```

### Verifying a Beacon proxy

To verify the Beacon proxy and the underlying information, you have to verify two contracts: the `Vault` (implementation) and OpenZepplin's `UpgradableBeacon`:

```ts
 await tenderly.verify(
  {
    name: "Vault",
    address: await getImplementationAddressFromBeacon(
      ethers.provider,
      beacon.address
    ),
  },
  {
    name: "UpgradeableBeacon",
    address: beacon.address,
  }
);
```

#### Complete code sample

```ts
import { getImplementationAddressFromBeacon } from "@openzeppelin/upgrades-core";
import { ethers, tenderly, upgrades } from "hardhat";
import { BeaconProxy, UpgradeableBeacon } from "../typechain-types";

describe("Vault", () => {
  it("beacon proxy deployment and verification", async () => {
    const VaultFactory = await ethers.getContractFactory("Vault");
    const TokenFactory = await ethers.getContractFactory("TToken");

    const token = await TokenFactory.deploy();
    await token.deployed();

    await tenderly.verify({
      name: "TToken",
      address: token.address,
    });

    let beacon = (await upgrades.deployBeacon(
      VaultFactory
    )) as UpgradeableBeacon;

    await beacon.deployed();

    let vault = await upgrades.deployBeaconProxy(
      beacon,
      VaultFactory,
      [token.address],
      {
        initializer: "initialize",
      }
    );
    await vault.deployed();

    console.log("Deployed beacon ", {
      proxy: beacon.address,
      implementation: await getImplementationAddressFromBeacon(
        ethers.provider,
        beacon.address
      ),
      beacon: beacon.address,
    });

    await tenderly.verify(
      {
        name: "Vault",
        address: await getImplementationAddressFromBeacon(
          ethers.provider,
          beacon.address
        ),
      },
      {
        name: "UpgradeableBeacon",
        address: beacon.address,
      }
    );

    console.log(
      `Vault version before upgrade: ${await VaultFactory.attach(
        await beacon.implementation()
      ).version()}`
    );

    const vaultV2Factory = await ethers.getContractFactory("VaultV2");

    // upgrade
    vault = await upgrades.deployBeaconProxy(beacon, vaultV2Factory, [
      token.address,
    ]);

    await upgrades.upgradeBeacon(beacon.address, vaultV2Factory, {});

    console.log("Upgraded beacon ", {
      proxy: beacon.address,
      implementation: await getImplementationAddressFromBeacon(
        ethers.provider,
        beacon.address
      ),
      beacon: beacon.address,
    });

    await tenderly.verify({
      name: "VaultV2",
      address: await getImplementationAddressFromBeacon(
        ethers.provider,
        beacon.address
      ),
    });

    console.log(
      `Vault version after upgrade: ${await VaultFactory.attach(
        await beacon.implementation()
      ).version()}`
    );
  });
});
```
