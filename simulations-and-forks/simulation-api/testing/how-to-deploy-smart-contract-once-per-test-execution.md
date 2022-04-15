# How to deploy smart contract once per test execution

Here we’ll extract the `fork-deploy` code to a separate function for reusability to `forkAndDeployGreeter`.

This is pretty self-explanatory - we create a Fork and deploy smart contracts to it in each individual test, before issuing transactions. You can think of it as a Fork dedicated to one and only one test.

This way each test function gets a clean contract with an unmodified state - the one present after initialization. Here we have level isolation of smart contracts under test. It’s pretty much how you’d want to test a class/service - having it cleanly initialized for each test you have.&#x20;

{% hint style="info" %}
Note that deployment time may significantly increase depending on the number of smart contracts you have.
{% endhint %}

It’s advisable to remove the Fork upon successful completion of the test by executing `fork.removeFork()` at the very end of each test (`it` or `afterEach`). The first approach keeps the Fork in case of test failure, which is handy for examination. The latter will remove the Fork even if your test fails.&#x20;

These tests provide the highest level of isolation, and transactions remain persisted. Individual tests have corresponding Forks visible in Tenderly Dashboard.

{% hint style="info" %}
Speed of test suites using this approach may become an issue, as the time it takes to run such a suite is $$O(N_TN_{SC})$$. You can find one proposed solution [here](reset-transactions-after-completing-the-test.md).
{% endhint %}

```tsx
import { fail } from "assert";
import { expect } from "chai";
import { ethers } from "hardhat";
import { forkForTest } from "./fork";

/** a reusable function to deploy the contract under test to the newly created fork */
const forkAndDeployGreeter = async () => {
  const fork = await forkForTest({ network_id: "1", block_number: 14386016 });
  // deploy the contract

  const Greeter = await ethers.getContractFactory(
    "Greeter",
    fork.provider.getSigner()
  );
  const greeter = await Greeter.deploy("Hello, world!");

  await greeter.deployed();
  return { fork, greeter }
}

describe("Greeter", function () {
  it("Should return the new greeting once it's changed", async function () {
	  // fork and deploy greeter to the fork
    const { fork, greeter } = await forkAndDeployGreeter();
    expect(await greeter.greet()).to.be.equal("Hello, world!");

    await (await greeter.setGreeting("Bonjour le monde!")).wait();
    expect(await greeter.greet()).to.be.equal("Bonjour le monde!");

		// remove the fork each time test succeeds
    fork.removeFork();
  });

  it("Should also return the new greeting once it's changed", async function () {
    const { fork, greeter } = await forkAndDeployGreeter();
    const secondGreeter = fork.signers[1];

    await (
      await greeter
        .connect(secondGreeter)
        .setGreeting("Hola, mundo!")
    ).wait();

    expect(await greeter.greet()).to.equal("Hola, mundo!");
    await fork.removeFork();
  });

});
```
