---
description: Learn how to integrate DevNets into your Continuous Integration (CI) pipeline.
---

# Setting Up DevNets for Continuous Integration

Continuous Integration (CI) automates the process of building, testing, and deploying smart contracts when you make a code change. Setting up CI for your smart contract project ensures that your code is always tested and verified before deployment.

### Why integrate DevNet into your CI

1. **Isolated testing environment**: DevNet allows you to test your smart contracts in an isolated environment, reducing the risk of interference from other test environments or team members working on the same project. This ensures that your tests are accurate, consistent, and reliable, making it an essential tool for developing robust and high-quality smart contracts.
2. **Consistent and automated testing**: Every code change is automatically tested, providing immediate feedback on whether the change introduces any errors or vulnerabilities. This helps maintain high code quality and reduces the risk of deploying faulty contracts to production.
3. **Debugger integration**: Easily integrate Tenderly Debugger into your workflow to efficiently identify, diagnose, and fix issues in your code. Debugger allows you to quickly address problems and ensure that your smart contracts are robust and secure.
4. **Reduced setup time**: Eliminate the need to manually set up and maintain a separate development network for smart contract testing. This saves time and resources, allowing you to focus on writing and testing your smart contracts rather than managing infrastructure.
5. **Ensures latest chain state**: Access to the most recent chain state for the chosen network or state from a specific point in time. This enables accurate testing and validation of your project's progress, resulting in a more reliable development workflow.
6. **Cost and resource efficiency**: Running CI tests on a DevNet is generally more cost-effective than using a public testnet or Mainnet. This eliminate the need to to mention host your own Mainnet fork where you might need to acquire test tokens or pay for gas. DevNet enable a more efficient use of computational resources, making it an excellent choice for development and testing.

### GitHub Actions

GitHub Actions is a CI/CD platform provided by GitHub that allows you to automate your workflow directly within your GitHub repository. To set up GitHub Actions for your smart contract project using DevNets, follow these steps:

1. Create a **`.github/workflows`** directory in your project repository if it doesn't already exist.
2. Create a new YAML file for your GitHub Actions workflow, such as **`smart-contract-ci.yml`**, in the **`.github/workflows`** directory.
3. Populate the YAML file with the following content:

```
name: Smart Contract CI

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: 16

      - name: Install dependencies
        run: yarn install
        working-directory: ./CI-project

      - name: Install Tenderly CLI
        run: curl <https://raw.githubusercontent.com/Tenderly/tenderly-cli/master/scripts/install-linux.sh> | sudo sh

      - name: Run tests
        run: yarn run test:devnet
        working-directory: ./CI-project
        env:
          TENDERLY_ACCESS_KEY: ${{ secrets.TENDERLY_ACCESS_KEY }}
```

4. Add the DevNet JSON-RPC URL as a secret in your GitHub repository by going to the repository's "Settings" > "Secrets" > "New repository secret." Name the secret **`DEVNET_JSON_RPC_URL`** and set its value to the JSON-RPC URL you obtained from Tenderly.
5. I you need to specify

For further reference, check out [this example on GitHub](https://github.com/Tenderly/devnet-examples/tree/main/CI-project).

### **CircleCI**

CircleCI is a CI/CD platform that automates the build, test, and deployment process for your projects. To set up CircleCI for your smart contract project using DevNet, follow these steps:

1. Sign up for a [**CircleCI account**](https://circleci.com/signup/) if you haven't already.
2. Add your project repository to CircleCI by navigating to the "Add Projects" tab and selecting the repository.
3. Create a **`.circleci`** folder in your project directory, and within that folder, create a **`config.yml`** file to configure your CI pipeline.
4. Configure the **`config.yml`** file with the following content, adjusting the commands and paths as needed for your specific project:

```yaml
version: 2.1
jobs:
  build:
    docker:
      - image: circleci/node:16
    steps:
      - checkout
      - run:
          name: Install Dependencies
          command: yarn install
          working_directory: ./CI-project

      - run:
            name: Install Tenderly CLI
            command: curl <https://raw.githubusercontent.com/Tenderly/tenderly-cli/master/scripts/install-linux.sh> | sudo sh

      - run:
          name: Run Tests
          command: yarn run test:devnet
          working_directory: ./CI-project

workflows:
  version: 2
  build-deploy:
    jobs:
      - build
```

In the example above, we are using the Node.js v16 image provided by CircleCI. Replace the **`command`** in the "Run Tests" step with the appropriate command for your project.

For further reference, check out [this example on GitHub](https://github.com/Tenderly/devnet-examples/tree/main/CI-project).
