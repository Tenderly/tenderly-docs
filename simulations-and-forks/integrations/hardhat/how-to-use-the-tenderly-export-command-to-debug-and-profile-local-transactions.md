# How to use the \`tenderly export\` command to debug and profile local transactions

Let’s make a small change to the sample script:

```text
// We require the Hardhat Runtime Environment explicitly here. This is optional 
// but useful for running the script in a standalone fashion through `node <script>`.
// When running the script with `hardhat run <script>` you'll find the Hardhat
// Runtime Environment's members available in the global scope.
const hre = require("@nomiclabs/hardhat");

async function main() {
// Hardhat always runs the compile task when running scripts through it. 
// If this runs in a standalone fashion you may want to call compile manually 
// to make sure everything is compiled
// await hre.run('compile');

// We get the contract to deploy
const Greeter = await hre.ethers.getContractFactory("Greeter");
const greeter = await Greeter.deploy("Hello, Hardhat!");

await greeter.deployed();

await hre.tenderly.persistArtifacts({
name: "Greeter",
address:greeter.address
});

console.log("Greeter deployed to:", greeter.address);

console.log("Changing greeting");

await greeter.setGreeting("Zdravo, Graditelju!");

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

As you can see, we added lines 21 through 26, where we’re changing the default greeting. Let’s re-run the script: `npx hardhat run --network local scripts/sample-script.js`. You’ll notice the new transaction appears on the **hardhat node** terminal.

It’s time to export some transactions! Firstly, run the **export init** command to set it up:

```text
tenderly export init
✔ Choose the name for the exported network: hardhat
✔ Super Awesome Project
✔ Enter rpc address (default: 127.0.0.1:8545):
✔ None
```

Finally, run `tenderly export` with the transaction hash and see the magic happen:

```text
tenderly export 0x0c8cab68f5d84dfdc02c903ef8c9f26c957a8e788e8b398e462f459ae1f6da47
Collecting network information...

Collecting transaction information...

Collecting contracts...
Successfully exported transaction with hash 0x0c8cab68f5d84dfdc02c903ef8c9f26c957a8e788e8b398e462f459ae1f6da47
You can view your transaction at <https://dashboard.tenderly.co/MyAwesomeUsername/super-awesome-project/local-transactions/69d3194e-6cca-47d4-b875-41d11fea5701>
```

By clicking on the provided link, you’ll have access to all of the Tenderly tools you know and love for that local transaction!

