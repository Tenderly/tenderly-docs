# First Usage of Tenderly APIs in Tests

### Create a fresh Fork from code

Let’s fork the **Ethereum** **Mainnet** on block number **14386016**. In order to do this, we’ll create a Fork we’ll test with in the cloud.

The bare minimum you’d want for your tests is in the following snippet:

```jsx
// the network and block where Tenderly fork gets created
const forkingPoint = { network_id: "1", block_number: 14386016 };

// an axios instance to make requests to Tenderly, for re-use purposes
const axiosOnTenderly = axios.create({
  baseURL: "https://api.tenderly.co/api/v1",
  headers: {
      "X-Access-Key": process.env.TENDERLY_ACCESS_KEY || "",
      "Content-Type": "application/json",
  },
});

const projectUrl = `account/${process.env.TENDERLY_USER}/project/${process.env.TENDERLY_PROJECT}`;

// create the specified fork programmatically in your project
const forkResponse = await axiosOnTenderly.post(`${projectUrl}/fork`, fork);
const forkId = forkResponse.data.root_transaction.fork_id;
console.info("Forked with fork id:", forkId)
// create the provider you can use throughout the rest of your test
const provider = new JsonRpcProvider(`https://rpc.tenderly.co/fork/${forkId}`);
```

With the Fork we created programatically, we get a JSON-RPC URL: `https://rpc.tenderly.co/fork/${forkId}`

We can use it later with your library of our choice.

{% hint style="info" %}
&#x20;Tenderly will create 10 test addresses with 100 ETH for testing. Any transaction signing will be done by the 0th address as the default signer.
{% endhint %}

### How to deploy a Smart Contract on the Fork from test code

Take notice that you’ll have to specify the `signer` provided by the `provider` representing the Tenderly JSON-RPC provider. This way, the ethers’ contract factory deploys the contract to the Tenderly fork:

```tsx
const Greeter = await ethers.getContractFactory(
  "Greeter",
  provider.getSigner() // use the provider
);
const greeter = await Greeter.deploy("Hello, world!");
await greeter.deployed();
```

Since the `deploy` call is a transaction in its own right, it’s signed by the default signer (0th address). In effect, the 0th test address is the deployer of the contract. You can do things differently, as we’ll see in a bit.

### How to perform an interaction with the smart contract

Here we’re using ethers, so interaction goes the standard way. To interact with the smart contract, i.e. calling functions (`greet`) and sending transactions (`setGreeting`), you can simply call these methods on the `greeter` contract reference. Any transactions will be signed by the 0th test account Tenderly provides, who is also the owner of the contract:

```tsx
// asserting to it
expect(await greeter.greet()).to.be.equal("Hello, world!");
await (await greeter.setGreeting("Hola, mundo!")).wait();
expect(await greeter.greet()).to.be.equal("Hola, mundo!");
```

### How to have a different address sign the transaction

This is also a well-known way to use ethers. When a Fork is created, the response from Tenderly’s `POST $project/fork` contains a list of created test accounts for that Fork, contained in `data.simulation_fork.accounts`. It’s a map from the address to the balance of that address - so you need to obtain the address and ask your provider to give you a corresponding signer object.&#x20;

This way it’s possible to make a transaction using an arbitrary signer:

```tsx
// sign with a specific signer
const testAddresses = Object.keys(forkResponse.data.simulation_fork.accounts);
const anotherSigner = provider.getSigner(testAddresses[2]);

await (
  await greeter
    .connect(anotherSigner)
    .setGreeting("Bonjour le monde!")
).wait();
expect(await greeter.greet()).to.be.equal("Bonjour le monde!");
```

### How to delete a Fork after a successful test

It’d be pretty great to delete any Forks after your automated tests are complete if you don’t intend to examine transactions and execution via Tenderly anymore. You can achieve this by doing the following:

```tsx
await axiosOnTenderly.delete(`${projectUrl}/fork/${forkId}`);
```

Deleting a Fork in effect removes everything done with it - all contracts deployed to it and all transactions executed against it.
