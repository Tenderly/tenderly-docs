---
description: >-
  Learn how to set up a CI/CD pipeline to automatically run smart contract tests
  on top of production data. Also, find out how to create a staging FE
  environment for PRs automatically.
---

# CI/CD Pipeline for Smart Contracts

## Overview

Learn how to set up Github Actions with Tenderly Forks to automate smart contract testing and staging deployment. Find out how to start from an empty project and end up with a valid CI/CD for your project.&#x20;

**Automatically run smart contract tests on top of production network data:**

1. Set up smart contract project infra.
2. Create a testing Github Action YAML file.
3. Inject a Tenderly Fork into the testing process.

**Automatically create a staging FE environment for PRs:**

1. Create a Github Action for FE web hosting.
2. Inject a Tenderly Fork into the building process.

## **Automatically run smart contract tests on top production network data**

### Set up smart contract project infra

Let’s create a dummy Solidity smart contract project and run some dummy tests using Hardhat. We can use Hardhat’s quick start guide to achieve this:

{% embed url="https://hardhat.org/getting-started#quick-start" %}

Additionally, we're going to extend networks with Tenderly Fork specification for the example below:

**Hardhat config:**

```tsx
import "@nomiclabs/hardhat-waffle";
import "@tenderly/hardhat-tenderly";
import "dotenv/config";

const {
    TENDERLY_FORK_URL
} = process.env

export default {
  solidity: "0.8.4",
  networks: {
    "tenderly-fork": {
      url: TENDERLY_FORK_URL
    },
  },
};
```

**`package.json`**

```json
...
"scripts": {
    "test": "npx hardhat test",
    "test:ci": "npx hardhat test --network tenderly-fork"
},
...
```

### Create a testing Github Action Workflow YAML file

Let's see how we can set up our Github Action to run our tests:

```yaml
name: Run tests in Tenderly Fork

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
jobs:
  test:
    name: Test hardhat-core on Ubuntu with Node ${{ matrix.node }}
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: ./ci-cd-pipeline-for-smart-contracts/smart-contract-pipeline
    strategy:
      matrix:
        node: [ 16 ]
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: ${{ matrix.node }}
      - uses: actions/cache@v2
        with:
          path: '**/node_modules'
          key: ${{ runner.os }}-modules-${{ hashFiles('**/yarn.lock') }}
      - name: Install
        run: yarn install
      - name: Run tests
        run: yarn test
```

### Inject a Tenderly Fork into the testing process

Finally, let’s see how we can inject a Tenderly Fork into our CI pipeline.

```yaml
      ...
- name: Run test on fork
	run: yarn test:ci
	env:
          JSON_RPC_URL: ${{ secrets.TENDERLY_FORK_URL }}
```

And we're done! 🎉

## **Automatically create a staging FE environment for PRs**

To create a staging FE environment for PRs automatically, we first need to:

### Create a Github Action for web hosting

Let’s create an action that would store the build distribution of our React application on the Google Cloud Storage bucket so we can access it later.

We need `GCP_CREDENTIALS` which you can generate using the command below. Once generated, you should store it as part of GitHub secrets.

```json
gcloud iam service-accounts keys create ~/key.json --iam-account <iam-name>@<project-id>.iam.gserviceaccount.com
```

**Github Action YAML**

```yaml
name: Build and deploy staging to google could storage
on:
  pull_request:
    branches: [ main ]
jobs:
  build-deploy:
    runs-on: ubuntu-latest
    defaults:
      run:
        working-directory: ./ci-cd-pipeline-for-smart-contracts/front-end-cd
    strategy:
      matrix:
        node: [ 16 ]
    steps:
      - uses: actions/checkout@v2
      - uses: actions/setup-node@v2
        with:
          node-version: ${{ matrix.node }}
      - uses: actions/cache@v2
        with:
          path: '**/node_modules'
          key: ${{ runner.os }}-modules-${{ hashFiles('**/yarn.lock') }}
      - id: 'auth'
        uses: 'google-github-actions/auth@v0'
        with:
          credentials_json: '${{ secrets.GCP_CREDENTIALS }}'
      - name: 'Set up Cloud SDK'
        uses: 'google-github-actions/setup-gcloud@v0'
      - name: Build React App
        run: yarn install && yarn run build
      - name: Deploy app build to GCS bucket
        run: |-
          gsutil -m rsync -R ./build gs://${{secrets.GCS_BUCKET}}/${{github.run_id}}
```

### Inject a Tenderly Fork into the building process

Now that we have our GitHub Action ready to roll, let’s edit it a bit to ensure it's aware of Tenderly Forks.

```yaml
 ...
- name: Build React App
  run: yarn install && yarn run build:cd
  env:
    TENDERLY_FORK_URL: ${{ secrets.TENDERLY_FORK_URL }}
    REACT_APP_ENV: staging
...
```

{% hint style="success" %}
Here are the links to the [source code](https://github.com/Tenderly/integration-samples/tree/main/ci-cd-pipeline-for-smart-contracts) and [GitHub Actions YAML](https://github.com/Tenderly/integration-samples/tree/main/.github/workflows).
{% endhint %}
