---
description: >-
  Follow a step-by-step guide and a cheat sheet of CLI commands for
  initializing, building, and deploying Web3 Actions.
---

# CLI Cheatsheet

This guide shows the commands you need to initialize, build, and deploy a Web3 Action project using Tenderly CLI.

**Step 1: Install the Tenderly CLI**

Use the `curl` command to download and install the Tenderly CLI binary on your local machine.

Install on macOS:

```bash
curl https://raw.githubusercontent.com/Tenderly/tenderly-cli/master/scripts/install-macos.sh | sh
```

Install on Linux:

```bash
curl https://raw.githubusercontent.com/Tenderly/tenderly-cli/master/scripts/install-linux.sh | sh
```

**Step 2: Log in to Tenderly via the CLI**

Log into the Tenderly CLI with your credentials by running this command:

```bash
tenderly login
```

**Step 3: Initialize a Web3 Actions project**

To initialize a Web3 Action project, run this command:

```bash
tenderly actions init
```

You can change the default initialization settings with two flags: change the name of the root Web3 Actions folder (default: `actions`) and the language for writing Action functions (default: `typescript` or `javascript`).

```bash
tenderly actions init --sources=actions --language=typescript
```

You’ll be prompted to add your Web3 Actions to a Tenderly project. You can either create a new project or pick an existing one.

**Step 3**: **Install any NPM dependency you need**

After running `tenderly init`, you have an NPM project at your disposal, so you can install any NPM library you need in a familiar way.

```bash
cd actions
npm i --save-dev axios ethers
cd ..
```

**Step 4: Build and deploy Web3 Actions**

After you have written your function and trigger configuration in **tenderly.yaml**, you can run these commands to build and deploy the Web3 Action.

```bash
# run within the folder containing tenderly.yaml

# Build the project (optional)
tenderly actions build

# Publish the project to Tenderly without running it (start manually)
tenderly actions publish

# Deploy the project to Tenderly Runtime (or re-deploy any changes you make)
tenderly actions deploy
```

Shortly after running `publish`, your Web3 Action is available in the Dashboard and listening to events per your configuration.

{% hint style="info" %}
You can upgrade your Web3 Actions with zero downtime, by running the `publish` command after you’ve edited the function and trigger configuration.
{% endhint %}

**Optional: Using Tenderly Runtime locally**

Install the [**@tenderly/actions-test**](https://github.com/Tenderly/tenderly-actions/tree/main/packages/actions-test) package to test your Web3 Action Functions locally.

Assuming you're already in an npm project, run the following:

```bash
npm install @tenderly/actions-test
```

{% hint style="info" %}
It’s recommended to keep tests and run scripts for web3-actions outside of the actions directory, to avoid increasing the size of your Web3 Actions project.
{% endhint %}

Check out a [guide on local development and testing of Web3 Actions](local-development-and-testing.md) for more detail and examples.
