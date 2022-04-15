# Testing

Here you'll find examples showing how to utilize Tenderly to achieve testing against Mainnet data, with no need for a local node and ability to integrate other capabilities of Tenderly in your testing process.

[**Local tests on top of Mainnet data in the Cloud**](local-tests-on-top-of-mainnet-data-in-the-cloud/) **** shows how to run your local tests against Mainnet data while transactions your tests do are simulated on a Tenderly Fork behind the scenes. Here you can also see a very basic **** [**first usage of Tenderly API in tests**](local-tests-on-top-of-mainnet-data-in-the-cloud/first-usage-of-tenderly-apis-in-tests.md).&#x20;



The following how-to list might give you more ideas about everything that is possible to test with Tenderly:

{% content-ref url="how-to-deploy-smart-contract-once-per-test.md" %}
[how-to-deploy-smart-contract-once-per-test.md](how-to-deploy-smart-contract-once-per-test.md)
{% endcontent-ref %}

...in order to test the contract.

{% content-ref url="deploy-smart-contracts-once-per-test-suite-execution.md" %}
[deploy-smart-contracts-once-per-test-suite-execution.md](deploy-smart-contracts-once-per-test-suite-execution.md)
{% endcontent-ref %}

...in order to optimize test suite run-time.

{% content-ref url="reset-transactions-after-completing-the-test.md" %}
[reset-transactions-after-completing-the-test.md](reset-transactions-after-completing-the-test.md)
{% endcontent-ref %}

...in order to isolate individual tests in a test suite.

{% hint style="success" %}
The code to these examples can be found in this [GitHub repo](https://github.com/Tenderly/integration-samples/tree/main/testing-tenderly-hardhat-ts).
{% endhint %}
