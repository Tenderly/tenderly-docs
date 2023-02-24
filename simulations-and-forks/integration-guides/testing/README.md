---
description: >-
  Learn how to use Tenderly Forks as testing infrastructure and optimize the
  process of running smart contract tests.
---

# Using Forks as Testing Infrastructure

The examples below show how to use Tenderly to achieve testing against actual Mainnet data with ease. Additionally, you can integrate other Tenderly capabilities into your testing process without needing a local node.

[**Local tests on top of Mainnet data in the Cloud**](local-tests-on-top-of-mainnet-data-in-the-cloud/) **** give a high-level overview of running your local tests against Mainnet data.&#x20;

Start by exploring the basic **** [**first usage of Tenderly API in tests**](local-tests-on-top-of-mainnet-data-in-the-cloud/first-usage-of-tenderly-apis-in-tests.md), **** where transactions performed by your tests are simulated on a Tenderly Fork behind the scenes.

### Testing with Tenderly

Explore the following how-to guides for ideas on how to use Tenderly for testing purposes. Learn how to:

1. Deploy and test a contract&#x20;

{% content-ref url="how-to-deploy-smart-contract-once-per-test.md" %}
[how-to-deploy-smart-contract-once-per-test.md](how-to-deploy-smart-contract-once-per-test.md)
{% endcontent-ref %}

2. Deploy a contract and optimize the test suite runtime

{% content-ref url="deploy-smart-contracts-once-per-test-suite-execution.md" %}
[deploy-smart-contracts-once-per-test-suite-execution.md](deploy-smart-contracts-once-per-test-suite-execution.md)
{% endcontent-ref %}

3. Reset transactions to isolate individual tests in a test suite&#x20;

{% content-ref url="reset-transactions-after-completing-the-test.md" %}
[reset-transactions-after-completing-the-test.md](reset-transactions-after-completing-the-test.md)
{% endcontent-ref %}

{% hint style="success" %}
The code for these examples can be found in this [GitHub repo](https://github.com/Tenderly/integration-samples/tree/main/testing-tenderly-hardhat-ts).
{% endhint %}
