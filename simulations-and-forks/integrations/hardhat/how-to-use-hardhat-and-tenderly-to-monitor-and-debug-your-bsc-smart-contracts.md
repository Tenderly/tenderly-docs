# How to use Hardhat and Tenderly to monitor and debug your BSC Smart Contracts

To start things out, we need a project with a contract we want to deploy. I will be using the default Hardhat example for this. To do this, we will run the following:

```text
yarn add hardhat

...

npx hardhat
```

Next up we'll install the `@tenderly/hardhat-tenderly` plugin in order to verify the contract we deploy:

```text
yarn add @tenderly/hardhat-tenderly
```

After this, we must edit our `hardhat.config.js` to include information about the BSC testnet:

```text
require("@nomiclabs/hardhat-waffle");
require("@tenderly/hardhat-tenderly")

module.exports = {
  solidity: "0.7.3",
  networks: {
    mumbai: {
      url: '<https://data-seed-prebsc-1-s1.binance.org:8545>',
      accounts: {
        mnemonic: {{env.mnemonic}},
      },
    },
  },
};
```

Finally all we need to is modify the deployment script in order to add the verify step and an example transaction:

```text
const hre = require("hardhat");

async function main() {
  const Greeter = await hre.ethers.getContractFactory("Greeter");
  const greeter = await Greeter.deploy("Hello, Hardhat!");

  await greeter.deployed();

  await greeter.setGreeting("Hello, BSC!")

  await hre.tenderly.verify({
      name: "Greeter",
      address: greeter.address
  })

  console.log("Greeter deployed to:", greeter.address);
}

main()
  .then(() => process.exit(0))
  .catch(error => {
    console.error(error);
    process.exit(1);
  });
```

This will output the url to the verified contract.

