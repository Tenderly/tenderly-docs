# How to push and verify Smart Contracts directly through code

You might be thinking to yourself: “Verifying and pushing Smart Contracts after each deployment is quite repetitive and prone to errors!”. You aren’t far from the truth. That’s why you can verify and push contracts directly inside of your Hardhat scripts!

```text
// We require the Hardhat Runtime Environment explicitly here. This is optional 
// but useful for running the script in a standalone fashion through `node <script>`.
// When running the script with `hardhat run <script>` you'll find the Hardhat
// Runtime Environment's members available in the global scope.
const hre = require("hardhat");

async function main() {
  // Hardhat always runs the compile task when running scripts through it.
    // If this runs in a standalone fashion you may want to call compile manually
    // to make sure everything is compiled
    // await hre.run('compile');

  // We get the contract to deploy
  const Greeter = await hre.ethers.getContractFactory("Greeter");
  const greeter = await Greeter.deploy("Hello, Hardhat!");

  await greeter.deployed();

  console.log("Greeter deployed to:", greeter.address);
  
  await hre.tenderly.persistArtifacts({
    name: "Greeter",
    address: greeter.address
  });
  
  await hre.tenderly.verify({
    name: "Greeter",
    address: greeter.address,
  })

  console.log("Changing greeting");

  await greeter.setGreeting("Zdravo, Hardhetu!");

  console.log("Greeting changed!");
}

// We recommend this pattern to be able to use async/await everywhere
// and properly handle errors.
main()
  .then(() => process.exit(0))
  .catch(error => {
    console.error(error);
    process.exit(1);
  });
```

If you look at line 26, you’ll see that with a simple `tenderly.verify()` or `tenderly.push()` call we can verify/push \(multiple\) Smart Contracts!

