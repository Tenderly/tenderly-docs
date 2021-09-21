# Using CLI to create a Project and push your Smart Contracts to Tenderly

First things first, we need to get your Smart Contracts into Tenderly to use all of the timesaving features like the Visual Debugger, Gas Profiler, Alerts, and more.

There are a couple of ways we can achieve this: we can use the Tenderly CLI to push contracts to a project, or we can verify our Smart Contracts on Etherscan and then paste in the address into Tenderly. I'm going to go with the first approach.

I already have the CLI installed locally, but if you don't have it already, [it's effortless to set up](https://github.com/Tenderly/tenderly-cli?utm_source=blog&utm_medium=post&utm_campaign=10_ways&utm_content=cli_setup#installation). Once you have it installed, run **tenderly login**.

The next step is to go into your project directory and run **tenderly init**. As I'm using the Tennis Match example from a previous article, I'm going to pick _Create new project_ and write _Tennis Match_.

```text
$ tenderly init
✔ Create new project
✔ Project: Tennis Match
Project successfully initialized. You can change the project information by editing the tenderly.yaml file or by rerunning tenderly init with the --re-init flag.
```

That's it! Your project is all set up, and you can push it for the first time to Tenderly.

In order for Tenderly to monitor your Smart Contracts in real-time, you need to push them to your dashboard. Pushing your Smart Contracts is as easy as running the **tenderly push** command. Let's try it now:

```text
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

Now when you open your [Tenderly dashboard](https://dashboard.tenderly.co/?utm_source=blog&utm_medium=post&utm_campaign=10_ways&utm_content=your_tenderly_dashboard), you'll see your newly created project, and your Smart Contracts added!

