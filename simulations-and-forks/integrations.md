# Integrations

## HardHat

{% hint style="info" %}
You can also check out our complete article on the topic of integrating HardHat with Tenderly [here](http://blog.tenderly.co/level-up-your-smart-contract-productivity-using-hardhat-and-tenderly/).
{% endhint %}

### How to setup HardHat

First things first, we need to add Hardhat into our project. You can follow along in an empty directory (we’ll be using yarn):

```
yarn add hardhat
```

Next up, we’ll initiate our project by using the `npx hardhat` command:

```
888    888                      888 888               888
888    888                      888 888               888
888    888                      888 888               888
8888888888  8888b.  888d888 .d88888 88888b.   8888b.  888888
888    888     "88b 888P"  d88" 888 888 "88b     "88b 888
888    888 .d888888 888    888  888 888  888 .d888888 888
888    888 888  888 888    Y88b 888 888  888 888  888 Y88b.
888    888 "Y888888 888     "Y88888 888  888 "Y888888  "Y888

👷 Welcome to Hardhat v2.0.0-rc.1 👷‍

✔ What do you want to do? · Create a sample project
✔ Hardhat project root: · /src/super-awesome-project
✔ Do you want to add a .gitignore? (Y/n) · y
✔ Help us improve Hardhat with anonymous crash reports & basic usage data? (Y/n) · true
✔ Do you want to install the sample project's dependencies with yarn (@nomiclabs/hardhat-waffle ethereum-waffle chai @nomiclabs/hardhat-ethers ethers)? (Y/n) · y
```

And we have a sample project set up! You can run **npx hardhat test** to check if everything is working.

### Integrating Tenderly with HardHat

Now that we have the Hardhat project all set up, it’s time to add Tenderly into the mix. We’ll be installing the **hardhat-tenderly** plugin and [the Tenderly CLI](https://github.com/tenderly/tenderly-cli#installation), which we’ll be using later:

```
yarn add @tenderly/hardhat-tenderly
brew tap tenderly/tenderly
brew install tenderly
```

As you can see, we used **brew** to install Tenderly. You can find the [alternative installation steps here](https://github.com/tenderly/tenderly-cli#installation).

To let know Hardhat to load the Tenderly plugin, add the following line to your `hardhat.config.js`:

```
require("@tenderly/hardhat-tenderly")
```

Next up, we can use the CLI to authenticate our development machine with our Tenderly dashboard (if you don’t already have an account, [you can register here](https://dashboard.tenderly.co/register)):

```
tenderly login
✔ Email
✔ Enter your email: me@email.co
✔ Password: ************
```

To do the final configuration step, you’ll need to tell Hardhat which Tenderly project to connect with. You can do that by adding the following snippet of code into the `hardhat.config.js` `module.exports`:

```
{
	tenderly: {
		username: "MyAwesomeUsername",
		project: "super-awesome-project"
	}
}
```

You can find the username and project by opening up [https://dashboard.tenderly.co](https://dashboard.tenderly.co), and copying from the URL [_https://dashboard.tenderly.co/{**USERNAME**}/{**PROJECT**_](https://dashboard.tenderly.co/%7BUSERNAME%7D/%7BPROJECT)_}._ Alternatively, you can run `tenderly whoami` to get the needed information.

The Tenderly plugin is now good to go!

### Deploying your contracts via ethers.js

When you initialized your Hardhat project, there were a couple of default files generated in your project. Put your attention towards the `./contracts/Greeter.sol` and `./scripts/sample-script.js` files.

* **Greeter.sol:** Contains a straightforward Smart Contract we’ll be using for this walkthrough
* **sample-scripts.js:** Contains a [deployment script](https://hardhat.org/getting-started/#deploying-your-contracts) for the Greeter Smart Contract

To deploy the Greeter, you should use the `npx hardhat run` command, which takes the script as the argument:

```
npx hardhat run ./scripts/sample-script.js
All contracts have already been compiled, skipping compilation.
Deploying a Greeter with greeting: Hello, Hardhat!
Greeter deployed to: 0x7c2C195CD6D34B8F845992d380aADB2730bB9C6F
```

This will successfully deploy the Greeter Smart Contract to the local **in-memory** Hardhat node. Keeping that in mind, let’s see how to set a more permanent solution so we can play around.

Open another terminal window and type in `npx hardhat node`. This will start a node against which we can run transactions. Now, edit your `hardhat.config.js` file and add the following to the `module.exports`:

```
{
	networks: {
		local: {
			url: 'http://127.0.0.1:8545'
	  	}
	}
}
```

To use the newly defined network, run the script with the following command:

```
npx hardhat run --network local scripts/sample-script.js
```

You’ll see logs popping up on the terminal which is running the Hardhat node.

### Debug and profile local transactions with `tenderly export`

Let’s make a small change to the sample script:

```
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

```
tenderly export init
✔ Choose the name for the exported network: hardhat
✔ Super Awesome Project
✔ Enter rpc address (default: 127.0.0.1:8545):
✔ None
```

Finally, run `tenderly export` with the transaction hash and see the magic happen:

```
tenderly export 0x0c8cab68f5d84dfdc02c903ef8c9f26c957a8e788e8b398e462f459ae1f6da47
Collecting network information...

Collecting transaction information...

Collecting contracts...
Successfully exported transaction with hash 0x0c8cab68f5d84dfdc02c903ef8c9f26c957a8e788e8b398e462f459ae1f6da47
You can view your transaction at <https://dashboard.tenderly.co/MyAwesomeUsername/super-awesome-project/local-transactions/69d3194e-6cca-47d4-b875-41d11fea5701>
```

By clicking on the provided link, you’ll have access to all of the Tenderly tools you know and love for that local transaction!

### Push and verify contracts with hardhat-tenderly tasks

Let’s say that we’re happy with our Greeter and want to test it out on a testnet. I’ll be using the Kovan testnet. To set it up, we’ll once again edit our `hardhat.config.js` file and add a new entry to the **networks** map:

```
{
    networks: {
		local: {
			url: 'http://127.0.0.1:8545'
		},
		kovan: {
			url: '<link-to-node>',
			mnemonic: '<mnemonic-phrase>'
		}
	}
}
```

To deploy the Smart Contract, we will run the script again, but with a minor change:

```
npx hardhat run --network kovan scripts/sample-script.js
```

As you can see, we need to set **kovan** as the target network for the script. Once the deployment is done, we will copy the outputted address and use it with the verify command:

```
npx hardhat --network kovan tenderly:verify Greeter=0x6f49F890B6B10AA49AF925625662439db6E8aFb8
```

If we navigate to the [Smart Contracts page](https://dashboard.tenderly.co/contract/kovan/0x6f49F890B6B10AA49AF925625662439db6E8aFb8), we’ll see we’ve successfully done the verification! Note that you can provide multiple `Contract=Address` pairs separated by a space character.

The `push` and `verify` commands are similar at first glance, but they’re quite different:

* **tenderly:verify: Publicly verifies the contracts for all Tenderly users.** This means that everyone has access to the source code of this Smart Contract.
* **tenderly:push: Privately adds the contracts to the project defined in hardhat.config.js.** This means no one except the people with access to the project can see the source code of this Smart Contract

### Push and verify contracts directly through code

You might be thinking to yourself: “Verifying and pushing Smart Contracts after each deployment is quite repetitive and prone to errors!”. You aren’t far from the truth. That’s why you can verify and push contracts directly inside of your Hardhat scripts!

```
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

If you look at line 26, you’ll see that with a simple `tenderly.verify()` or `tenderly.push()` call we can verify/push (multiple) Smart Contracts!

### How to monitor and debug your BCS contracts

To start things out, we need a project with a contract we want to deploy. I will be using the default Hardhat example for this. To do this, we will run the following:

```
yarn add hardhat

...

npx hardhat
```

Next up we'll install the `@tenderly/hardhat-tenderly` plugin in order to verify the contract we deploy:

```
yarn add @tenderly/hardhat-tenderly
```

After this, we must edit our `hardhat.config.js` to include information about the BSC testnet:

```
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

```
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

This will output the URL to the verified contract.

## Truffle

By the end of this guide, you will be all set up with a development environment that uses Truffle and Tenderly to speed up your Smart Contract development process.

{% hint style="info" %}
Note: The `proxy` command is now deprecated in favor of the more powerful and versatile `export` command. You can read more about the `export` command [here](https://github.com/Tenderly/tenderly-cli#export).
{% endhint %}

We are going to make a simple calculator and use it to debug any problems we might encounter. If you already have Truffle installed and configured, you can skip to the Contract section below.

To install the Truffle framework just run the following command:

```
$ npm install -g truffle
```

Now let’s create the directory for our calculator project and initialize truffle:

```
$ mkdir calculator
$ cd calculator
$ truffle init
Downloading...
Unpacking...
Setting up...
Unbox successful. Sweet!

Commands:

Compile:        truffle compile
  Migrate:        truffle migrate
  Test contracts: truffle test
```

### The Contract <a href="#the-contract" id="the-contract"></a>

Our calculator supports just addition, subtraction, multiplication and division.

```
pragma solidity ^0.4.24;

contract Calculator {
    uint c;

    function add(uint a, uint b) public {
        c = a + b;
    }

    function sub(uint a, uint b) public {
        c = a - b;
    }

    function mul(uint a, uint b) public {
        c = a * b;
    }

    function div(uint a, uint b) public {
        require(b > 0, "The second parameter should be larger than 0");

        c = a / b;
    }

    function getResult() public view returns (uint x) {
        return c;
    }
}
```

We can check if our code is correct by running the compile Truffle command:

```
$ truffle compile
Compiling ./contracts/Calculator.sol...
Compiling ./contracts/Migrations.sol...
Writing artifacts to ./build/contracts
```

### Deploying the Calculator Contract <a href="#deploying-the-calculator-contract" id="deploying-the-calculator-contract"></a>

We have no use of our contract if it just lays there on our filesystem! Let’s deploy it to a local Ganache node and test it out! To install Ganache run the following command:

```
$ npm install -g ganache-cli
```

Now that we have Ganache installed, we can set up our network configuration in truffle.js:

```
module.exports = {
  networks: {
    ganache: {
      host: "127.0.0.1",
      port: 8545,
      network_id: "*",
    },
    tenderly: {
      host: "127.0.0.1",
      port: 9545,
      network_id: "*",
      gasPrice: 0
    }
  },
};
```

Before we deploy our Smart Contract we have to start Ganache by running:

```
$ ganache-cli

Ganache CLI v6.2.3 (ganache-core: 2.3.1)

Available Accounts
==================
(0) 0xa439c978fab0e2b13a874dc6c48dbc79c6f6655e (~100 ETH)

...
```

Then we make a new migration under `./migrations/2_deploy_calculator.js`:

```
var Calculator = artifacts.require('Calculator');

module.exports = function (deployer) {
  deployer.deploy(Calculator);
};
```

And finally to deploy the Calculator Smart Contract we can run:

```
$ truffle migrate --network ganache
Using network 'ganache'.

Running migration: 1_initial_migration.js
  Deploying Migrations...
  ... 0x92039ee2c2f057dfb2b180bb532fb767626d4e1092a98125209f8f51c300818b
  Migrations: 0x492649777fbe2e25f0470834f7ab50291c329391
Saving successful migration to network...
  ... 0xd57f3537cc224426ee86c0d0ada172c0a5c7a4f40921b1bb8d5997d5e8ffde01
Saving artifacts...
Running migration: 2_deploy_calculator.js
  Deploying Calculator...
```

### Interacting with the Smart Contract <a href="#interacting-with-the-smart-contract" id="interacting-with-the-smart-contract"></a>

Later on, we are going to write some tests, but for now, let’s interact with our contract directly:

```
$ truffle console --network ganache
truffle(ganache)> var calculatorInstance;
truffle(ganache)> Calculator.deployed().then(instance => calculatorInstance = instance)
truffle(ganache)> calculatorInstance.mul(10,5)
truffle(ganache)> calculatorInstance.getResult()
BigNumber { s: 1, e: 1, c: [ 50 ] }
```

As we can see we got the correct result! It’s an expensive calculator, but damn it it’s a distributed one!

However, what happens if we call the contract with invalid arguments? What if we maybe divide by zero?

```
$ truffle console --network ganache
truffle(ganache)> var calculatorInstance;
truffle(ganache)> Calculator.deployed().then(instance => calculatorInstance = instance)
truffle(ganache)> calculatorInstance.div(10,0)
Error: VM Exception while processing transaction: invalid opcode
    at XMLHttpRequest._onHttpResponseEnd (/Users/user/.config/yarn/global/node_modules/truffle/build/webpack:/~/xhr2/lib/xhr2.js:509:1)
    at XMLHttpRequest._setReadyState (/Users/user/.config/yarn/global/node_modules/truffle/build/webpack:/~/xhr2/lib/xhr2.js:354:1)
...
```

If you look at the error we received you will see that there isn’t much helpful information. In the next section, we will write tests for the div function and use Tenderly to see how it helps with cases like this one.

### Installing Tenderly <a href="#installing-tenderly" id="installing-tenderly"></a>

The Tenderly CLI is a Go program, so we compile just a single binary that you can download and use. The basic installation process would be to download [the latest binary from the releases page](https://github.com/Tenderly/tenderly-cli/releases/latest) and move it somewhere in your $PATH so you can use it globally.

For everyone’s convenience, we have simplified the process explained above so you can install the Tenderly CLI just by running the following commands.

#### Installing on macOS <a href="#installing-on-macos" id="installing-on-macos"></a>

Via [Homebrew](https://brew.sh):

```
$ brew tap tenderly/tenderly
$ brew install tenderly
```

Alternatively, via cURL (the command downloads the latest release and moves it to /usr/local/bin):

```
$ curl https://raw.githubusercontent.com/Tenderly/tenderly-cli/master/scripts/install-macos.sh | sh
```

#### Installing on Linux <a href="#installing-on-linux" id="installing-on-linux"></a>

The command downloads the latest release and moves it to/usr/local/bin:

```
$ curl https://raw.githubusercontent.com/Tenderly/tenderly-cli/master/scripts/install-linux.sh | sh
```

#### Installing on Windows <a href="#installing-on-windows" id="installing-on-windows"></a>

Go to the [tenderly-cli](https://github.com/Tenderly/tenderly-cli/releases) release page, download the latest version and put it somewhere in your $PATH.

### Using Tenderly for debugging <a href="#using-tenderly-for-debugging" id="using-tenderly-for-debugging"></a>

Now that we have the CLI all set up we can easily find why the smart contract is failing. First, we start the CLI with the proxy command which proxies requests to an Ethereum node and turns unusable errors which we saw into stack traces that we can use for easier debugging.

For the sake of speed, I’m going to use Ganache locally, but you can use Kovan or any other testnet if you want. You can see which options are supported by the CLI by running tenderly proxy --help:

```
$ tenderly proxy --help
Creates a server that proxies rpc requests to Ethereum node and builds a stacktrace in case error occurs during the execution time

Usage:
  tenderly proxy [flags]

Flags:
  -h, --help                   help for proxy
      --path string            Path to the project build folder. (default ".")
      --proxy-host string      Call host. (default "127.0.0.1")
      --proxy-port string      Call port. (default "9545")
      --target-host string     Blockchain rpc host. (default "127.0.0.1")
      --target-port string     Blockchain rpc port. (default "8545")
      --target-schema string   Blockchain rpc schema. (default "http")
```

Because we're using Ganache with the default options, we won’t pass any arguments, and will just run the proxy command from the root of the project:

```
$ tenderly proxy
server will run on 127.0.0.1:9545
redirecting to 127.0.0.1:8545
```

Now that we have everything set up let’s go back to the console and try out our contract again, but this time we pass--network tenderly when starting the console:

```
$ truffle console --network tenderly
truffle(tenderly)> var calculatorInstance;
truffle(tenderly)> Calculator.deployed().then((instance) => calculatorInstance = instance)
truffle(tenderly)> calculatorInstance.div(10, 0)
Error: 0x0 Error: INVALID OPCODE, execution stopped
    at a / b
        in Calculator:19

    at XMLHttpRequest._onHttpResponseEnd (/Users/user/.config/yarn/global/node_modules/truffle/build/webpack:/~/xhr2/lib/xhr2.js:509:1)
...
```

![This the the error we get when we don’t proxy our requests through the Tenderly CLI](<../.gitbook/assets/image (45).png>)

![And this is the human readable stack trace we get when we do proxy our requests thru the Tenderly CLI](<../.gitbook/assets/image (23).png>)

### Writing the tests and fixing the contract <a href="#writing-the-tests-and-fixing-the-contract" id="writing-the-tests-and-fixing-the-contract"></a>

Because we now know precisely on which line the problem is, we can write a test case and then fix the issue. So let’s make the `./test/calculator.js` file and write out the test:

```
var Calculator = artifacts.require("./Calculator.sol");

contract('Calculator', function (accounts) {
  it("shouldn't allow division by zero", async function () {
    const fail = await Calculator.new();
    await fail.div(5, 0);
  });
});
```

We can run the truffle test --network tenderly command to see if we’ve set up everything properly:

![](<../.gitbook/assets/image (31).png>)

You can see that we get a stack trace that gives us enough information to fix the issue.

Let’s add the require statement as the first line of the div function to fix our division by zero edge case:

```
require(b > 0, "The second parameter should be larger than 0");
```

And let’s update our test with the assertions that assure we are seeing expected behaviour:

```
var Calculator = artifacts.require("./Calculator.sol");

contract('Calculator', function (accounts) {
  it("shouldn't allow division by zero", async function () {
    let error;
    const fail = await Calculator.new();
    try {
      await fail.div(5, 0);
    } catch (e) {
      error = e;
    }

    assert.isDefined(error, "No exception thrown during divison");
    assert.isTrue(error.message.search("revert") >= 0, "Expected transaction revert");
  });
});
```

If we run our tests we should see everything is working as it should:

```
truffle test --network ganache
Using network 'ganache'.

Compiling ./contracts/Calculator.sol...


  Contract: Calculator
    ✓ shouldn't allow division by zero (91ms)


  1 passing (131ms)
```

## Remix

As Remix has a concept for plugins, we will go through everything that is needed to use it with Tenderly.

Using the file structure plugin we navigate to the Storage.sol contract which we will be deploying.

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.29.45.png>)

We will first compile the contract:

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.31.05.png>)

We also have the deployment plugin which we will use to deploy this contract to Kovan:

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.32.32.png>)

Next, we can install the Tenderly plugin found here:

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.33.36.png>)

In order to connect with Tenderly you will need an **access token** which you can get by going to your Tenderly dashboard and in the top right clicking on Settings, and then going to the Authorizations tab where you will generate a new access token for Remix:

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.37.11.png>)

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.38.50.png>)

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.39.18.png>)

Now you just need to paste the access token into Remix:

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.40.39.png>)

You will now be able to choose whether to add the contract to an existing project by choosing from a list or create a new one. Now, in order to verify and add the contract into your project, you will need to click on the **verify** tab in Remix, choose the network and contract, as well as copy the address of the deployed contract. In this case we will privately verify a contract on Tenderly:

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.46.51.png>)

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.47.50.png>)

You are also able to import contracts into Remix from your Tenderly project:

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.49.41.png>)

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.50.24.png>)

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.50.58.png>)

You can also add new contracts to your project and see them in Remix at any point. Let's say we want to add this Dai contract into our project in Tenderly. We will copy it's address, go back to the project we want to add it to and go through the flow:

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.52.54.png>)

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.53.50.png>)

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.54.54.png>)

Then if we go back in to Remix and refresh the contract list we will see the newly added contract. We can import it and now use it in Remix:

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.55.58.png>)

![](<../.gitbook/assets/Screenshot 2021-11-18 at 09.56.37.png>)

You can also use Remix with Visual Studio by using their VSCode extension, which supports the Tenderly plugin as well. [**You can find it here**](https://marketplace.visualstudio.com/items?itemName=RemixProject.ethereum-remix).
