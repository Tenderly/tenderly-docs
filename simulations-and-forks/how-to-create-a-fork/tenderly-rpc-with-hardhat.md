# Tenderly RPC (with HardHat)

### Part zero: The setup

We need to add the following to the `hardhat.config.js` file:

```
tenderly: {
    project: "",
    username: "",
    forkNetwork: "42" //Network id of the network we want to fork
  },
```

You can find the project name and username over at out [dashboard](https://dashboard.tenderly.co).

We also need to install the beta version of the @tenderly/hardhat-tenderly plugin:

```
yarn add @tenderly/hardhat-tenderly@1.1.0-beta.6
```

### Part one: The contract

To start off, we'll need a contract. Let's use a slightly modified version of the Hardhat Greeter contract:

```
//SPDX-License-Identifier: Unlicense
pragma solidity ^0.6.8;

import "hardhat/console.sol";

contract Greeter {
  string greeting;

  constructor(string memory _greeting) public {
    console.log("Deploying a Greeter with greeting:", _greeting);
    greeting = _greeting;
  }

  function greet() public view returns (string memory) {
    return greeting;
  }

  function setGreetingThrow(string memory _greeting) public {
    assert(1 == 2);
    console.log("Changing greeting from '%s' to '%s'", greeting, _greeting);
    greeting = _greeting;
  }

  function setGreeting(string memory _greeting) public {
    console.log("Changing greeting from '%s' to '%s'", greeting, _greeting);
    greeting = _greeting;
  }
}
```

We have added a method that will cause the transaction to revert due to an impossible assertion.

### Part two: The test

Now for the test suite:

```
describe("Greeter", function () {
    let postDeployHead
    let provider
    let greeter

    before(async () => {
        //Initialize the provider
				await tenderly.network().initializeFork()
				//Wrap the provider
        provider = new ethers.providers.Web3Provider(tenderly.network())
        //Set the ethers provider to the one we initialized so it targets the correct backend
        ethers.provider = provider
        //deploy contracts and set head to post deployment head from tenderly.network()
        const Greeter = await ethers.getContractFactory("Greeter")
        greeter = await Greeter.deploy("Hello, Hardhat!");
        await greeter.deployed()
        postDeployHead = tenderly.network().getHead()
    })

    beforeEach(() => {
        //set current head back to after deployment, effectively resetting the contracts on the fork
        tenderly.network().setHead(postDeployHead)
    })

    //This will properly update the greeting
    it("Should return the new greeting once it's changed", async function () {
        expect(await greeter.greet()).to.equal("Hello, Hardhat!");
        await greeter.setGreeting("Hola, mundo!");
        expect(await greeter.greet()).to.equal("Hola, mundo!");
    })

    //This test will fail, since the transaction reverts, and we reset the head back to the original state in beforeEach
    it("Should throw", async function () {
        expect(await greeter.greet()).to.equal("Hello, Hardhat!");
        await greeter.setGreetingThrow("this will throw")
        expect(await greeter.greet()).to.equal("Hola, mundo!");
    })
});
```

Let's break it down a little:

1.  Before:

    ```
    before(async () => {
            //Initialize the provider
            provider = new ethers.providers.Web3Provider(tenderly.network())
            //Set the ethers provider to the one we initialized so it targets the correct backend
            ethers.provider = provider
            //deploy contracts and set head to post deployment head from tenderly.network()
            const Greeter = await ethers.getContractFactory("Greeter")
            greeter = await Greeter.deploy("Hello, Hardhat!");
            await greeter.deployed()
            postDeployHead = tenderly.network().getHead()
        })
    ```

    In the before block we will be deploying our contracts, but before we do so, we need to tell ethers to use the proper provider. The first two lines of code will set the tenderly.network() object (that is injected by Hardhat) as the active provider.

    Now, every time we use ethers, it will be referencing our RPC node in the background.

    Once we finish deploying, all we need to do is store the head (or root). We will use this later.\

2.  BeforeEach:

    ```
    beforeEach(() => {
            //set current head back to after deployment, effectively resetting the contracts on the fork
            tenderly.network().setHead(postDeployHead)
        })
    ```

    We will revert the current state of the provider back to the state it was at after we deployed the contracts. In effect, this will revert any changes on the contracts caused by the test without having to redeploy it.\

3.  The tests:

    ```
    //This will properly update the greeting
        it("Should return the new greeting once it's changed", async function () {
            expect(await greeter.greet()).to.equal("Hello, Hardhat!");
            await greeter.setGreeting("Hola, mundo!");
            expect(await greeter.greet()).to.equal("Hola, mundo!");
        })
    ```

    The first test case will update the greeting and check if it was updated correctly. This test will pass, and in the background will move the head of the provider to a state after the `setGreeting()` transaction is completed.

    ```
    //This test will fail, since the transaction reverts, and we reset the head back to the original state in beforeEach
        it("Should throw", async function () {
            expect(await greeter.greet()).to.equal("Hello, Hardhat!");
            await greeter.setGreetingThrow("this will throw")
            expect(await greeter.greet()).to.equal("Hola, mundo!");
        })
    ```

    This test will fail. Since the state is reset in beforeEach, the modification we've made in the previous test will have no effect.

### Part three: The analysis

That's all well and good, but what if we want to inspect the transaction that failed?

In that case our before function will need a slight modification:

```
before(async () => {
        //Initialize the provider
        provider = new ethers.providers.Web3Provider(tenderly.network())
        //Set the ethers provider to the one we initialized so it targets the correct backend
        ethers.provider = provider
        //deploy contracts and set head to post deployment head from tenderly.network()
        const Greeter = await ethers.getContractFactory("Greeter")
        greeter = await Greeter.deploy("Hello, Hardhat!");
        await greeter.deployed()
        //Optionally we can verify the contracts ahead of time
        await tenderly.network().verify({
            name: "Greeter",
            address: greeter.address
        })
        postDeployHead = tenderly.network().getHead()
    })
```

Notice the call to `tenderly.network().verify()`. This will pass the source code to our backend and do the required processing in order to properly display transaction details.

Now, whenever a transaction fails, we can simply generate a link:

```
const transactionLink = `https://dashboard.tenderly.co/${username}/${project}/fork/${tenderly.network().getFork()}/simulation/${tenderly.network().getHead()}`
```

For example, we can log this link in an afterEach hook.

Opening it in a browser will allow us to inspect the transaction via the Tenderly visual debugger.
