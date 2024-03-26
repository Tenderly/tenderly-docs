---
description: >-
  Tenderly Sandbox is a fast prototyping environment where you can write,
  execute, and debug smart contracts in the browser using Solidity and
  JavaScript.
---

# 🪣 Tenderly Sandbox

[**Tenderly Sandbox**](https://sandbox.tenderly.co/) is a fast prototyping environment for Solidity smart contracts. As a plug-and-play solution for smart contract development, the Sandbox comes with Solidity and JavaScript editors that run in your browser. Since each Sandbox has a unique URL, you can easily [share it with others or embed it](tenderly-sandbox.md#sharing-and-embedding-your-sandbox) in any HTML document.

The Sandbox also eliminates the need to install anything locally to run your code. Code execution is handled by your browser and Tenderly infrastructure, allowing you to write, run, and debug your smart contract code instantly.

The purpose of the Sandbox is to lower the barriers to entry for beginner blockchain developers. Similarly, educators and tutorial creators can use Sandbox to quickly demonstrate how Solidity and JavaScript are used in smart contract development.

### **How does the Sandbox work?**

The Sandbox is comprised of two code editors: **Solidity editor** and **JavaScript editor**.

At the most basic level, Sandbox compiles your Solidity code and executes your JavaScript code against it to call your smart contracts. Your JavaScript code is executed in your browser while the execution of the compiled Solidity code is handled by [Tenderly Forks](https://docs.tenderly.co/simulations-and-forks/how-to-create-a-fork).

Each time you run the Sandbox, a temporary Fork is created in the background along with 10 Ethereum accounts, each with a 100 ETH balance which you can use to send transactions on the Fork.

After running the Sandbox, execution results are displayed in the console output panel, along with the list of transactions that have occurred. Any transaction can be loaded into the Tenderly platform with a single click, giving you access to the [Debugger](https://docs.tenderly.co/debugger/how-to-use-tenderly-debugger) and visibility into the execution trace, state changes, gas usage, etc.

### Getting familiar with the Sandbox UI

<figure><img src=".gitbook/assets/sandbox_main_920_520" alt="tenderly sandbox user interface"><figcaption><p>Sandbox user interface</p></figcaption></figure>

The Sandbox UI consists of four panels:

* **Solidity editor (top left) —** write or paste in your Solidity smart contract code here. It’s possible to write several contracts in a single file. All of them will be compiled and accessible from JavaScript.
* **JavaScript editor (top right)** — write or paste in your JavaScript code that deploys the smart contracts and interacts with them.
* **JavaScript console output (bottom right) —** this is where you’ll see the results of the JavaScript execution as well as any errors that have occurred along the way.
* **Transactions overview (bottom left)** — a list of transactions that have occurred as a result of your Solidity and JavaScript code, as well as an easy way to load any transaction into the Debugger and inspect the executing trace and much more.

### Launching and running your first Sandbox

**Step 1:** [Create an account](https://dashboard.tenderly.co/register) on Tenderly if you don’t have one already.

{% hint style="info" %}
While you don’t need an account to play around in the Sandbox, creating one unlocks additional features. Registered users can save, share, and embed their Sandbox environment.
{% endhint %}

**Step 2:** Visit [**sandbox.tenderly.co**](http://sandbox.tenderly.co) and navigate to the dropdown next to the logo in the top nav bar. From the dropdown, click on **New Sandbox**. Give your Sandbox a unique name and click **Save**.

**Step 3:** When you create a new Sandbox, the top two panels will be populated with a HelloWorld smart contract and JavaScript code example. You can delete the example from both panels and write or paste in your custom Solidity and JavaScript code.

**Step 4:** Optionally, configure your Sandbox by selecting the network, block, compiler version, and setting compiler optimizations. (See [**Customizing your Sandbox environment**](tenderly-sandbox.md#customizing-your-sandbox-environment)).

**Step 5:** Click **Run** to compile the smart contract and execute your JavaScript code.

**Step 6:** Navigate to the Simulate Transactions panel (bottom left) to view a list of all the transactions that resulted from your smart contract. Click on any transaction to load it into the Tenderly Dashboard to inspect the execution trace or perform other debugging tasks.

#### Copying (forking) an existing Sandbox

To build on top of another user’s Sandbox and ensure your work is saved, you need to make a copy of the original Sandbox and add it to your account.

* **Step 1:** Open up the Sandbox you want to copy.
* **Step 2:** Click the **Create a Copy** button in the top nav bar.

You will automatically be forwarded to the copied version of the Sandbox saved to your account.

{% hint style="warning" %}
If you don’t create a copy, any changes you make to someone else’s Sandbox will be temporarily saved in your browser without affecting the original source. You can still edit and run the original Sandbox, but all your work will be lost once you refresh the page or exit the browser.
{% endhint %}

#### Managing your Sandboxes

To view a list of all the Sandboxes you created or copied, **click on the dropdown menu** next to the logo in the top nav bar. By default, all Sandboxes are publicly visible.&#x20;

Manage your Sandboxes by **clicking the three dots icon** next to the Sandbox name to perform any of the following actions:

* **Rename** — give your Sandbox a different name. The original URL slug of the Sandbox will remain unchanged.
* **Duplicate** — create a copy of the Sandbox.
* **Delete** — remove the Sandbox from your account. Deleted Sandboxes cannot be recovered.

### Customizing your Sandbox environment

<figure><img src=".gitbook/assets/sandbox_cinfig_920_520" alt="tenderly sandbox configuration options"><figcaption><p>Sandbox configuration options</p></figcaption></figure>

The Sandbox gives you several configuration options, allowing you to customize your environment to fit your technical requirements:

* **Network** — select one of the networks where you want to deploy your code.
* **Block** — run your code on the latest block or specify any block number.
* **Compiler version** — choose the Solidity compiler version compatible with your code.
* **Compiler optimizations** — enter the number of optimizations to be performed by the compiler or disable them altogether.

These configuration options are located above the transactions overview window or when you click on the **Configure** button.

### Using JavaScript to interact with smart contracts

The deploy and interact with your smart contracts with JavaScript, you can use [Ethers.js](https://docs.ethers.io) and [Web3.js](https://web3js.readthedocs.io/) libraries. Both libraries are included in the Sandbox by default and can be instantiated as `ethers` and `web3`, respectively.&#x20;

The examples below show you how to access your preferred library from the Sandbox.

[**Ethers.js Sandbox example**](https://sandbox.tenderly.co/examples/counter-ethers)

```jsx
const provider = new ethers.providers.JsonRpcProvider($rpcUrl);
```

[**Web3.js Sandbox example**](https://sandbox.tenderly.co/examples/counter-web3)

```jsx
let web3 = new Web3($rpcUrl);
```

#### Available JavaScript global variables

Below is a list of available JavaScript global variables that you can use anywhere in your code:

* `$rpcUrl` — global variable containing the URL of the Fork. Use it to connect to the Fork from Ethers.js/Web3.js and send transactions to the Fork.

```jsx
const provider = new ethers.providers.JsonRpcProvider($rpcUrl);
let web3 = new Web3($rpcUrl);
```

* `$contracts` — global variable providing access to a map of JSON objects representing compiled contracts, the ABI, bytecode, etc. The map is indexed with the names of the smart contracts defined in the Solidity file.

```jsx
const contract = $contracts["HelloWorld"];

const factory = new ethers.ContractFactory(
  contract.abi,
  contract.evm.bytecode,
  provider.getSigner()
);
const helloWorldContract = await factory.deploy("Hello World");
```

* `$accounts` — global variable containing a list of 10 Ethereum accounts created on the Fork. Each account has a balance of 100 ETH. Since a new Fork is created each time you run the Sandbox, the account addresses will also change, so make sure to reference an account by its index and not the actual account address.

```jsx
const account1Signer = provider.getSigner($accounts[1]);
const helloByAccount1 = await helloWorldContract.connect(account1Signer).get();
helloByAccount1.setGreeting("Hello, Moon!");
```

* `$fork` — JavaScript object containing low-level information about the Fork such as the included accounts, creation date, block number, network, etc.

#### Debugging JavaScript code

{% hint style="warning" %}
**JavaScript execution time is limited to 60 seconds.**

If your code takes longer to execute, or you spend too much time in the debugger, you’ll get a timeout error. If you need to increase the JavaScript execution time, contact Support by clicking the in-app Intercom button.
{% endhint %}

You can use the browser’s JavaScript debugger to debug your code. You must invoke the `debugger;` instruction, and open your browser’s Developer Tools. When you run the Sandbox, the debugger will activate at that instruction.

If Developer Tools are not active, the `debugger;` instruction will have no effect, and your code will run without interruptions.

```jsx
const account1Signer = provider.getSigner($accounts[1]);

debugger; // execution halts for debugging if Developer Tools are open
 
const helloByAccount1 = await helloWorldContract.connect(account1Signer).get();
helloByAccount1.setGreeting("Hello, Moon!");
```

### Dynamic imports of Solidity smart contracts

You can use dynamic imports to load external smart contracts into your Sandbox. This is useful if you need to import thousands of lines of code from another smart contract without having to copy/paste the code.

Only contracts coming from a scoped npm package can be imported using the import method.

```solidity
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

contract MyToken is ERC20 {
...
}
```

### Sharing and embedding your Sandbox

Follow the instructions below to get a sharable link and embed code for your Sandbox.&#x20;

#### Sharing a Sandbox

<figure><img src=".gitbook/assets/sandbox_sharing" alt=""><figcaption><p>Sandbox sharing options</p></figcaption></figure>

Share your Sandbox by clicking the **Share** button from the top nav bar. Four sharing options are available to you: via Twitter, email, Telegram, or you can copy the Sandbox URL and send it to someone directly.

#### Embedding a Sandbox

<figure><img src=".gitbook/assets/sandbox_embed920_520" alt=""><figcaption><p>Sandbox embedding options</p></figcaption></figure>

To embed your Sandbox on your website, blog, or any other place on the web, click on the **Embed** button from the dropdown. This will generate an `iframe` tag that you can embed inside another HTML document.

Customize which panels are displayed in the iframe by playing around with the **Customize** options. You can also choose which panel is displayed as the default from the **Choose Default Tab** dropdown.

When you make subsequent edits to your Sandbox code, the changes will be immediately reflected in the embedded iframe.

### Practical Sandbox examples

* [**HelloWorld** ](https://sandbox.tenderly.co/examples/hello-world)— beginner-friendly Sandbox showing you how to create a smart contract and execute a simple function.
* [**AAVE Flashloan**](https://sandbox.tenderly.co/examples/aave-flashloan) — advanced Sandbox that gives any potential user an insight into integrating with Aave and using this functionality. Learn how to execute a smart contract to take out a loan and pay it back by the time the transaction ends.
* [**BAYC Land Sale**](https://sandbox.tenderly.co/examples/bayc-land-contract-optimizations) — advanced Sandbox that demonstrates how careful smart contract optimizations can significantly reduce gas usage. The example outlines optimization steps that could have reduced the gas fee for minting BAYC NFTs by 30 to 40%. With a detailed overview, you can inspect each line of the code, make adjustments, and then run the optimized version.
