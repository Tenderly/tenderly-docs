# CI/CD pipeline for smart contracts

## Overview

You will see how to set up Github Actions with Tenderly Forks in order to achieve automated smart contract testing and staging deployment. We are going to showcase how to start from an empty project and end up with a valid CI/CD for your project. So, what are we going to do?&#x20;

**Automatically run smart contract tests on top of production network data:**

1. Setup smart contract project infra.
2. Create testing Github Actions YAML file.
3. Inject Tenderly Fork in the test process.

**Automatically create staging FE environment for PRs:**

1. Create Github Action for FE web hosting.
2. Inject Tenderly Fork in the build process.

## **Automatically run smart contract tests on top production network data**

### Setup smart contract project infra

Let’s create a dummy solidity smart contract project and some dummy tests using Hardhat. We can utilize Hardhat’s quick start guide in order to achieve this:

{% embed url="https://hardhat.org/getting-started#quick-start" %}

Additionally, we are going to extend networks with Tenderly Fork specification, for the example below:

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

### Create testing Github Action Workflow YAML file

Let's see how we can set up our Github Action in order to run our tests:

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

### Inject Tenderly Fork into the test process

And finally, let’s see how we can inject a Tenderly Fork into our CI pipeline.

```yaml
      ...
- name: Run test on fork
	run: yarn test:ci
	env:
          JSON_RPC_URL: ${{ secrets.TENDERLY_FORK_URL }}
```

And we are done! 🎉

## **Automatically create staging FE environment for PRs**

### Create Github Action for web hosting

Let’s create an action that would store the build distribution of our React application on the Google Cloud Storage bucket so we can access it later.

We will need `GCP_CREDENTIALS` which you can generate using the command below and you should store as part of GitHub secrets.

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

### Inject Tenderly Fork into the build process

Now that we have our GitHub Action ready to roll, let’s edit it a bit in order to be aware of Tenderly Forks.

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
Here are the links to the [source code](https://github.com/Tenderly/integration-samples/tree/main/ci-cd-pipeline-for-smart-contracts) and also [GitHub Actions YAML](https://github.com/Tenderly/integration-samples/tree/main/.github/workflows).
{% endhint %}
