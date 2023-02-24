---
description: >-
  Learn how to run local tests in the cloud and what a testing flow might look
  like when testing smart contracts deployed on Tenderly Forks.
---

# Local Tests on Top of Mainnet Data in the Cloud

## Overview

With Tenderly, you can create a staging or a QA environment. You can set up your automated tests to run in the cloud in the same way your dapp talks to a forked chain environment. In your automated QA process, you can leverage various Tenderly capabilities.

Here are some examples where you may find it useful:

* If your dapp has dependencies on external smart contracts, you can run your tests against a Fork to the latest state of your staging/QA environment or even the Mainnet. This way, you can find issues as they appear.
* You can parallelize the execution of a volume of test suites while using Tenderly’s cloud infrastructure instead of running a node of your own (e.g. using hardhat’s).
* You can test interacting with a smart contract already deployed on-chain (perhaps not even your own). You can investigate the execution of all participating smart contracts through Debugger, which can provide you with valuable insights especially when failures are present.
* You have a failing test on CI/CD. If you want to understand failures, you can direct the Web3 provider (ethers/web3js) to use Tenderly RPC and perform all operations through it.
* A part of your standard _`SETUP-TEST-ASSERT`_ cycle may be to simulate one or more transactions as in the _`SETUP`_ part so that you can test your contract in very specific circumstances.
* You want to deploy your contract on individual test levels, e.g. when you want to test around the deployment and initialization of smart contracts.
* You want to pre-deploy all your contracts on the test suite level, optimizing contract deployment time for tests, e.g. when you want to test a large number of contracts.

## Example testing workflow&#x20;

Here’s what a testing flow might look like when you include Tenderly in the process:

1. You create a Fork of an existing network either through the Tenderly Dashboard or using Tenderly API (going with the latter in case of automated tests).
2. You deploy the smart contracts you wish to test from the test code. You can do this on a test-suite basis or in each individual test.
3. After the test is complete, the best practice is to remove the Fork you created for it. Of course, in case of failing tests, you'd want to keep the Fork so you could inspect the reason it failed. You can do this in the Tenderly Dashboard, where you can obtain the information needed to understand the cause of failures.

## High-level overview

In these guides, we’ll lay out some steps needed to execute tests against smart contracts deployed on Tenderly Forks.

### Assumptions about the local environment

The code snippets below use the following libraries. We’re assuming Hardhat and ethers in the development environment to show how things work:

```tsx
import { JsonRpcProvider } from "@ethersproject/providers";
import axios from "axios";
import * as dotenv from "dotenv";
import { ethers } from "hardhat";

dotenv.config();
```

Check if you have `TENDERLY_PROJECT`, `TENDERLY_USER`, `TENDERLY_ACCESS_KEY` exposed in your code as described in [Configuration of API Access](../../../reference/configuration-of-api-access.md).

### The contract for testing

We're using a slightly modified Greeter smart contract for this example:

```solidity
//SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Greeter {
    string private greeting;
    address private owner;

    constructor(string memory _greeting) {
        greeting = _greeting;
        owner = msg.sender;
    }

    function greet() public view returns (string memory) {
        return greeting;
    }

    function setGreeting(string memory _greeting) public {
        greeting = _greeting;
    }

    function resetGreeting() public {
        require(msg.sender == owner, "Resettable only by the owner");
        greeting = "Hello, world";
    }
}
```
