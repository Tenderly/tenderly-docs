# How to deploy your contracts via ethers.js

When you initialized your Hardhat project, there were a couple of default files generated in your project. Put your attention towards the `./contracts/Greeter.sol` and `./scripts/sample-script.js` files.

* **Greeter.sol:** Contains a straightforward Smart Contract we’ll be using for this walkthrough
* **sample-scripts.js:** Contains a [deployment script](https://hardhat.org/getting-started/#deploying-your-contracts) for the Greeter Smart Contract

To deploy the Greeter, you should use the `npx hardhat run` command, which takes the script as the argument:

```text
npx hardhat run ./scripts/sample-script.js
All contracts have already been compiled, skipping compilation.
Deploying a Greeter with greeting: Hello, Hardhat!
Greeter deployed to: 0x7c2C195CD6D34B8F845992d380aADB2730bB9C6F
```

This will successfully deploy the Greeter Smart Contract to the local **in-memory** Hardhat node. Keeping that in mind, let’s see how to set a more permanent solution so we can play around.

Open another terminal window and type in `npx hardhat node`. This will start a node against which we can run transactions. Now, edit your `hardhat.config.js` file and add the following to the `module.exports`:

```text
{
	networks: {
		local: {
			url: 'http://127.0.0.1:8545'
	  	}
	}
}
```

To use the newly defined network, run the script with the following command:

```text
npx hardhat run --network local scripts/sample-script.js
```

You’ll see logs popping up on the terminal which is running the Hardhat node.

