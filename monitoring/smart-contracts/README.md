# Smart Contracts

## Adding a Contract to your Project via Tenderly Dashboard

{% hint style="info" %}
After deploying a contract to a Tenderly Fork using a JSON-RPC, REST API or a Simulation you can **** [**verify your contract**](../../simulations-and-forks/verifying-a-smart-contract.md) **** so Tenderly can decode everything into a human readable format.
{% endhint %}

There are several ways you can add a contract to your project from the Dashboard.

### Import public contract

&#x20;You can import any public (verified) contract by pasting the address...

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.02.53.png>)

... or by uploading a JSON...

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.03.54.png>)

... or by pasting the contract source from a file/uploading a source file...

![](<../../.gitbook/assets/Screenshot 2021-10-21 at 12.51.18.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.05.42.png>)

... or by uploading the source file itself.

### Uploading the source directory

By using the directory **** option, you can batch upload more than one contract at a time:

![](<../../.gitbook/assets/Screenshot 2021-10-21 at 12.51.18.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.08.41.png>)

If any of the files for verifying your contracts is missing you will be prompted to add them in the list of contract on top:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.10.00.png>)

You will be prompted to choose which contract to upload if the file contains multiple contracts, as well as to define the following:

* Which [network](../../getting-started.md) is the contract deployed to.
* What is the contract's address.
* (Optionally) add the library name and address for specific contracts that require them.

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.10.19.png>)

When your contract is added you can continue to add contracts from this screen via the **+ Add more** button:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.12.18.png>)

The last thing to do is to fill out the compiler info with the following parameters:

* Compiler Version (automatically refreshed list from Solidity GitHub).
* Optimizations Used (true/false).
* Optimization Count.
* EVM Version (latest is always the default).

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.12.54.png>)

{% hint style="warning" %}
Note that choosing the correct Compiler Version for your contract is important to avoid compiler (bytecode mismatch) errors.
{% endhint %}

### CLI Upload

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 16.14.47.png>)

### Adding a contract to your project via Tenderly CLI

First things first, we need to get your Smart Contracts into Tenderly to use all of the timesaving features like the Visual Debugger, Gas Profiler, Alerts, and more.

There are a couple of ways we can achieve this: we can use the Tenderly CLI to push contracts to a project, or we can verify our Smart Contracts on Etherscan and then paste in the address into Tenderly. Let's see how we'd do this via the CLI.

If you don't have the Tenderly CLI already installed, [it's effortless to set up](https://github.com/Tenderly/tenderly-cli#installation). Once you've done that, run **tenderly login**.

The next step is to go into your project directory and run **tenderly init**. As I'm using the Tennis Match example from a previous article, I'm going to pick _Create new project_ and write _Tennis Match_.

```
$ tenderly init
✔ Create new project
✔ Project: Tennis Match
Project successfully initialized. You can change the project information by editing the tenderly.yaml file or by rerunning tenderly init with the --re-init flag.
```

That's it! Your project is all set up, and you can push it for the first time to Tenderly.

In order for Tenderly to monitor your Smart Contracts in real-time, you need to push them to your dashboard. Pushing your Smart Contracts is as easy as running the **tenderly push** command. Let's try it now:

```
$ tenderly push
Setting up your project...
Analyzing Truffle configuration...

Pushing Smart Contracts for project: tennis-match
We have detected the following Smart Contracts:
• Migrations
• TennisMatch

Successfully pushed Smart Contracts for project tennis-match. You can view your contracts at https://dashboard.tenderly.dev/Habic/tennis-match/contracts

All Smart Contracts successfully pushed.
```

Now when you open your [Tenderly dashboard](https://dashboard.tenderly.co), you'll see your newly created project, and your Smart Contracts added!

{% content-ref url="public-contracts.md" %}
[public-contracts.md](public-contracts.md)
{% endcontent-ref %}

{% content-ref url="proxy-contracts.md" %}
[proxy-contracts.md](proxy-contracts.md)
{% endcontent-ref %}
