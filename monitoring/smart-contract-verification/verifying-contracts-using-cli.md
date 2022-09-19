# Verifying Contracts using CLI

First things first, we need to get your Smart Contracts into Tenderly to use all of the timesaving features like the Visual Debugger, Gas Profiler, Alerts, and more.

There are a couple of ways we can achieve this: we can use the Tenderly CLI to push contracts to a project, or we can verify our Smart Contracts on Etherscan and then paste in the address into Tenderly. Let's see how we'd do this via the CLI.

If you don't have the Tenderly CLI already installed, [it's effortless to set up](https://github.com/Tenderly/tenderly-cli?utm\_source=blog\&utm\_medium=post\&utm\_campaign=10\_ways\&utm\_content=cli\_setup#installation). Once you've done that, run **tenderly login**.

The next step is to go into your project directory and run **tenderly init**. As we're using the Tennis Match example from a previous article, we're going to pick _Create new project_ and write _Tennis Match_.

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

Now when you open your [Tenderly dashboard](https://dashboard.tenderly.co/?utm\_source=blog\&utm\_medium=post\&utm\_campaign=10\_ways\&utm\_content=your\_tenderly\_dashboard), you'll see your newly created project, and your Smart Contracts added!
