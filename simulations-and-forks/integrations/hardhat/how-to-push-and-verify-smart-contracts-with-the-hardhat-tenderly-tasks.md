# How to push and verify Smart Contracts with the hardhat-tenderly tasks

Let’s say that we’re happy with our Greeter and want to test it out on a testnet. I’ll be using the Kovan testnet. To set it up, we’ll once again edit our `hardhat.config.js` file and add a new entry to the **networks** map:

```text
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

```text
npx hardhat run --network kovan scripts/sample-script.js
```

As you can see, we need to set **kovan** as the target network for the script. Once the deployment is done, we will copy the outputted address and use it with the verify command:

```text
npx hardhat --network kovan tenderly:verify Greeter=0x6f49F890B6B10AA49AF925625662439db6E8aFb8
```

If we navigate to the [Smart Contracts page](https://dashboard.tenderly.co/contract/kovan/0x6f49F890B6B10AA49AF925625662439db6E8aFb8), we’ll see we’ve successfully done the verification! Note that you can provide multiple `Contract=Address` pairs separated by a space character.

The `push` and `verify` commands are similar at first glance, but they’re quite different:

* **tenderly:verify: Publicly verifies the contracts for all Tenderly users.** This means that everyone has access to the source code of this Smart Contract.
* **tenderly:push: Privately adds the contracts to the project defined in hardhat.config.js.** This means no one except the people with access to the project can see the source code of this Smart Contract.

