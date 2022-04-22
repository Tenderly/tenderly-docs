# Local Tests on top of Mainnet Data in the Cloud

## Overview

With Tenderly you can create a staging or a QA environment - in the same way your dApp talks to the forked chain environment, you can set up your automated tests to run in the cloud, and in your automated QA process you can leverage various capabilities Tenderly offers.

Here are some cases where you may find it useful:

* If your dApp has dependencies on external smart contracts, you can run your tests against a Fork to the latest state of your Staging/QA environment or even Mainnet, which can be very helpful in finding issues as they appear.
* You want to parallelize the execution of a volume of test suites while using Tenderly’s cloud infrastructure instead of running a node of your own (e.g. using hardhat’s).
* You can test interacting with a smart contract already deployed to the chain (perhaps not even your own), and investigate the execution of participating smart contracts through the Debugger, which can provide insights especially when failures are present.
* You have a failing test on CI/CD - if you want to understand failures, you can direct the Web3 provider (ethers/web3js) to use Tenderly RPC and perform all operations through it.
* A part of your standard _`SETUP-TEST-ASSERT`_ cycle may be to simulate one or more transactions as in the _`SETUP`_ part so that you can test your contract in very specific circumstances.
* Deploy your contract on individual test levels, e.g. when you want to test around deployment and initialization of smart contracts.
* Pre-deploy all your contracts on the test suite level, optimizing contract deployment time for tests, e.g. when you want to test a large number of contracts.

## Example testing workflow&#x20;

Here’s what a testing flow might look like when Tenderly is included in the process:

1. We create a Fork of an existing network either through the Tenderly Dashboard or using Tenderly API (going with the latter in case of automated tests).
2. We deploy the smart contracts we wish to test from the test code. We can do this on a test-suite basis or in each individual test.
3. After the test is complete, the best practice is to remove the Fork we created for it. Of course, in case of failing tests, we’d want to keep the Fork so we could inspect the reason it failed in the Tenderly Dashboard, where we can obtain information needed to understand what led to failures.

## High-level overview

In these guides we’ll lay out some steps needed in order to execute tests against smart contracts deployed on Tenderly forks.

### Assumptions about the local environment

The code snippets below will be using the following libraries. We’re assuming Hardhat and ethers in the development environment to show how things work:

```tsx
import { JsonRpcProvider } from "@ethersproject/providers";
import axios from "axios";
import * as dotenv from "dotenv";
import { ethers } from "hardhat";

dotenv.config();
```

Check if you have `TENDERLY_PROJECT`, `TENDERLY_USER`, `TENDERLY_ACCESS_KEY` exposed in your code as described in [Configuration of API Access](../../configuration-of-api-access.md).

### The contract we’ll be testing

We’ll be using a slightly modified Greeter smart contract for this example:

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
