# Tenderly Sandbox

Tenderly Sandbox is a fast-prototyping environment, using both existing and new features to allow you to test stuff quickly and comprehensively on multiple networks. You can also easily share your Sandbox with anyone, for collaboration or any other purposes.

Sandboxes are definitely beginner-friendly because of their ease of use. Educators creating Solidity, JavaScript, and Smart Contract tutorials can also use this feature to write and demonstrate code. Basically, this feature is suitable for anyone looking for a space for quick iterations that can easily be shared either publicly or with team members.

![](<../.gitbook/assets/image (77).png>)

### What can Sandboxes do?

An easy way to write, run and test smart contracts. Think of this as JSFiddle, but for blockchain development. Sandboxes allow you to run javascript code that can deploy and test smart contracts in an isolated environment powered by our Forks.&#x20;

Furthermore, you get the console output and a transaction list with metadata for every run. In case something unexpected happens there is always our flagship [**Debugger**](../debugger/how-to-use-tenderly-debugger/) that can help you resolve any issue.

### Sandbox Elements

**Smart Contract Editor** - create, fork and edit contracts.

**Javascript Editor** - create and edit JS scripts.

**Javascript Execution Output (Console)** - invoke and trigger smart contracts in order to display and analyze results from individual Javascript runs:

![](<../.gitbook/assets/image (97).png>)

**Overview of Executed Transactions** - a list of executed transactions with status, addresses and functions, and a quick way to jump into the [Transaction](../monitoring/contracts/) or [Execution Overview](../monitoring/contracts/execution-overview.md), [Debugger](../debugger/how-to-use-tenderly-debugger/) and more:

![](<../.gitbook/assets/image (86).png>)

You are also able to change the Network, Compiler and Optimizations settings, choose the Block Number for executions, as well as **easily share your whole Sandbox anyone**.

### Workflows

You can support many different workflows with Sandboxes, and some of those are:

**(1) Writing Smart Contracts** - a simple and intuitive workflow for Smart Contract creation, either from scratch or from a prior starting point by forking a specific deployed contract or a whole Sandbox. Think of it as a Golang playground.

**(2) Iterative Testing** - for those who are primarily interested in inspecting and testing already deployed contracts, so you can quickly and easily iterate on tweaking smaller pieces of Smart Contracts or JS scripts. Think of it as a "protocol developer trying to fix a bug in a deployed contract".

**(3) Sharing and Collaboration** - easily share your (or use other) Sandboxes, with intuitive input packaging for easy consumption for the reader/collaborator.

### (some) Sandbox Examples

**HelloWorld** - a great starting point for anyone using Tenderly Sandbox for the first time. Here, you can learn how to create a smart contract and execute a simple function:

{% embed url="https://sandbox.tenderly.co/examples/hello-world" %}

**AAVE Flashloan** - this example **** will give any potential user an insight into integrating with Aave and using this functionality. By following this example, you can see how to execute a smart contract to take out a loan and pay it back by the time the transaction ends:

{% embed url="https://sandbox.tenderly.co/examples/aave-flashloan" %}

**BAYC Land Sale** - **** showcases how careful and detailed contract optimization can significantly reduce gas usage. The example outlines optimization steps that could have reduced the gas fee for minting the BAYC NFTs by even 30-40%. With a detailed overview, you can inspect each line of the code, make adjustments, and then run the optimized version:

{% embed url="https://sandbox.tenderly.co/examples/bayc-land-contract-optimizations" %}
