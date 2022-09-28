# Automatic Contract Verification

Automatic contract verification is a part of Tenderly’s Hardhat plugin. This method of verification happens seamlessly when you’re deploying a contract using Ethers.js. The only additional step is to enable the automatic verification in Tenderly in your `hardhat.config.ts` file.

```tsx
// File: hardhat.config.ts
import * as tdly from "@tenderly/hardhat-tenderly";
tdly.setup({ automaticVerifications: true });
// automaticVerifications defaults to `true`, same as:
// tdly.setup();
```

The code example below deploys the `Greeter` contract and verifies it in Tenderly. The contract verification process is seamless, requiring no additional steps apart from deploying the contract.

```tsx
// File: scripts/greeter/automatic.ts
import { ethers } from "hardhat";

async function main() {
  const Greeter = await ethers.getContractFactory("Greeter");
  const greeter = await Greeter.deploy("Hello, Hardhat!");

  await greeter.deployed();

  console.log("{Greeter} deployed to", greeter.address);
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

Next, execute the Hardhat run command:

```bash
npx hardhat run scripts/greeter/automatic.ts --network ropsten
```

After executing the command, you’ll receive the following output:

![Output of npx hardhat run scripts/greeter/automatic.ts --network ropsten](<../../../.gitbook/assets/automatic terminal>)

To check whether the operation execution was successful, you should [access your Tenderly Dashboard](https://dashboard.tenderly.co/) by clicking the link printed in the console output.

In the Tenderly Dashboard, you should see something similar to the following.&#x20;

![Verified contract in Tenderly Dashboard](<../../../.gitbook/assets/automatic dashboard contract>)

When you click Add to Project, you’ll have an overview of the Greeter.sol with its source code. Next to it, you can see `console.sol` - a Solidity Library by Hardhat that was included automatically.

![Source code of the verified Contract added to a project](<../../../.gitbook/assets/image (5).png>)

## How automatic contract verification works

When you call Ethers’ `await greeter.deployed()`, the plugin will automatically detect the contract and its address, upload the source code, and let Tenderly verify against the contract deployed on the selected network.&#x20;

It will automatically detect all the libraries and contracts imported by the one you've just deployed, and include that information for verification.&#x20;

Essentially, automatic verification is a **no-code solution.**  This isn't the case with other verification methods.

## When is automatic verification applicable?

Automatic verification works only when deploying new contracts. If you’re working with a previously deployed Smart Contract, or you require a greater level of configuration control and flexibility, so you should explore [manual contract verification methods.](https://docs.tenderly.co/monitoring/contract-verification/verifying-contracts-using-the-tenderly-hardhat-plugin/manual-contract-verification)
