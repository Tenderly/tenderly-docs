# Truffle

By the end of this guide, you will be all set up with a development environment that uses Truffle and Tenderly to speed up your Smart Contract development process.

{% hint style="info" %}
Note: The `proxy` command is now deprecated in favor of the more powerful and versatile `export` command. You can read more about the `export` command [here](https://github.com/Tenderly/tenderly-cli#export).
{% endhint %}

We are going to make a simple calculator and use it to debug any problems we might encounter. If you already have Truffle installed and configured, you can skip to the Contract section below.

To install the Truffle framework just run the following command:

```text
$ npm install -g truffle
```

Now let’s create the directory for our calculator project and initialize truffle:

```text
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

### The Contract <a id="the-contract"></a>

Our calculator supports just addition, subtraction, multiplication and division.

```text
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

```text
$ truffle compile
Compiling ./contracts/Calculator.sol...
Compiling ./contracts/Migrations.sol...
Writing artifacts to ./build/contracts
```

### Deploying the Calculator Contract <a id="deploying-the-calculator-contract"></a>

We have no use of our contract if it just lays there on our filesystem! Let’s deploy it to a local Ganache node and test it out! To install Ganache run the following command:

```text
$ npm install -g ganache-cli
```

Now that we have Ganache installed, we can set up our network configuration in truffle.js:

```text
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

```text
$ ganache-cli

Ganache CLI v6.2.3 (ganache-core: 2.3.1)

Available Accounts
==================
(0) 0xa439c978fab0e2b13a874dc6c48dbc79c6f6655e (~100 ETH)

...
```

Then we make a new migration under `./migrations/2_deploy_calculator.js`:

```text
var Calculator = artifacts.require('Calculator');

module.exports = function (deployer) {
  deployer.deploy(Calculator);
};
```

And finally to deploy the Calculator Smart Contract we can run:

```text
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

### Interacting with the Smart Contract <a id="interacting-with-the-smart-contract"></a>

Later on, we are going to write some tests, but for now, let’s interact with our contract directly:

```text
$ truffle console --network ganache
truffle(ganache)> var calculatorInstance;
truffle(ganache)> Calculator.deployed().then(instance => calculatorInstance = instance)
truffle(ganache)> calculatorInstance.mul(10,5)
truffle(ganache)> calculatorInstance.getResult()
BigNumber { s: 1, e: 1, c: [ 50 ] }
```

As we can see we got the correct result! It’s an expensive calculator, but damn it it’s a distributed one!

However, what happens if we call the contract with invalid arguments? What if we maybe divide by zero?

```text
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

### Installing Tenderly <a id="installing-tenderly"></a>

The Tenderly CLI is a Go program, so we compile just a single binary that you can download and use. The basic installation process would be to download [the latest binary from the releases page](https://github.com/Tenderly/tenderly-cli/releases/latest) and move it somewhere in your $PATH so you can use it globally.

For everyone’s convenience, we have simplified the process explained above so you can install the Tenderly CLI just by running the following commands.

#### Installing on macOS <a id="installing-on-macos"></a>

Via [Homebrew](https://brew.sh/):

```text
$ brew tap tenderly/tenderly
$ brew install tenderly
```

Alternatively, via cURL \(the command downloads the latest release and moves it to /usr/local/bin\):

```text
$ curl https://raw.githubusercontent.com/Tenderly/tenderly-cli/master/scripts/install-macos.sh | sh
```

#### Installing on Linux <a id="installing-on-linux"></a>

The command downloads the latest release and moves it to/usr/local/bin:

```text
$ curl https://raw.githubusercontent.com/Tenderly/tenderly-cli/master/scripts/install-linux.sh | sh
```

#### Installing on Windows <a id="installing-on-windows"></a>

Go to the [tenderly-cli](https://github.com/Tenderly/tenderly-cli/releases) release page, download the latest version and put it somewhere in your $PATH.

### Using Tenderly for debugging <a id="using-tenderly-for-debugging"></a>

Now that we have the CLI all set up we can easily find why the smart contract is failing. First, we start the CLI with the proxy command which proxies requests to an Ethereum node and turns unusable errors which we saw into stack traces that we can use for easier debugging.

For the sake of speed, I’m going to use Ganache locally, but you can use Kovan or any other testnet if you want. You can see which options are supported by the CLI by running tenderly proxy --help:

```text
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

```text
$ tenderly proxy
server will run on 127.0.0.1:9545
redirecting to 127.0.0.1:8545
```

Now that we have everything set up let’s go back to the console and try out our contract again, but this time we pass--network tenderly when starting the console:

```text
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

![This the the error we get when we don&#x2019;t proxy our requests through the Tenderly CLI](../../.gitbook/assets/image%20%2833%29.png)

![And this is the human readable stack trace we get when we do proxy our requests thru the Tenderly CLI](../../.gitbook/assets/image%20%2815%29.png)

### Writing the tests and fixing the contract <a id="writing-the-tests-and-fixing-the-contract"></a>

Because we now know precisely on which line the problem is, we can write a test case and then fix the issue. So let’s make the `./test/calculator.js` file and write out the test:

```text
var Calculator = artifacts.require("./Calculator.sol");

contract('Calculator', function (accounts) {
  it("shouldn't allow division by zero", async function () {
    const fail = await Calculator.new();
    await fail.div(5, 0);
  });
});
```

We can run the truffle test --network tenderly command to see if we’ve set up everything properly:

![](../../.gitbook/assets/image%20%2821%29.png)

You can see that we get a stack trace that gives us enough information to fix the issue.

Let’s add the require statement as the first line of the div function to fix our division by zero edge case:

```text
require(b > 0, "The second parameter should be larger than 0");
```

And let’s update our test with the assertions that assure we are seeing expected behaviour:

```text
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

```text
truffle test --network ganache
Using network 'ganache'.

Compiling ./contracts/Calculator.sol...


  Contract: Calculator
    ✓ shouldn't allow division by zero (91ms)


  1 passing (131ms)
```

