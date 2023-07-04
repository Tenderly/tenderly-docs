---
description: Example of how to use DevNets in a Aave core.
---

# Using DevNets with Aave

### Introduction to Aave

Aave is a decentralized non-custodial liquidity markets protocol where users can participate as depositors or borrowers. Depositors provide liquidity to the market to earn a passive income, while borrowers are able to borrow in an overcollateralized (perpetually) or undercollateralized (one-block liquidity) fashion. Aave's open-source protocol offers features such as flash loans, rate switching, and more, making it a powerful tool for DeFi applications.

### Prerequisites

Before you start, make sure you have the following:

* Node.js installed on your system.
* Git installed on your system.
* An account with Tenderly.

### Steps to Integrate DevNets into Aave

1.  **Clone the Aave Project**: Start by cloning the Aave project from Tenderly. This will create a local copy of the project on your system. Run the following command in your terminal:

    ```
    git clone git@github.com:Tenderly/aave-v3-core-mirror.git
    ```
2.  **Set Up the Hardhat Config File**: Next, you'll need to set up the hardhat configuration file. This file is used to specify the network configuration for your project. Update the `networks` section as follows:

    ```
    networks: {
        ...
        devnet: {
            url: 'https://rpc.vnet.tenderly.co/. . .',
            hardfork: 'YOUR_HARDFORK',
            chainId: YOUR_HARDHAT_CHAINID,
            throwOnTransactionFailures: true,
            throwOnCallFailures: true,
        },
    }
    ```

    Replace `'YOUR_HARDFORK'` and `YOUR_HARDHAT_CHAINID` with the appropriate values for your project.
3.  **Run Hardhat Tests**: Finally, you can start running hardhat tests on your local system. Run the following command in your terminal:

    ```
    npm run test-devnet
    ```

    This command will run the test suite against the DevNet.

### Troubleshooting

If you encounter any issues during the integration process, please refer to the [Hardhat Troubleshooting Guide](https://hardhat.org/guides/troubleshooting.html) or the [Tenderly Documentation](https://docs.tenderly.co/).

### Next Steps

After successfully integrating DevNets into Aave, you can start developing and testing your DeFi applications. For more information on how to use Aave, refer to the [Aave Developers Documentation](https://developers.aave.com/).

### Additional Resources

* [Aave GitHub Repository](https://github.com/aave/aave-protocol)
* [Tenderly Aave Mirror Repository](https://github.com/Tenderly/aave-v3-core-mirror)

### Contact Information

For further assistance, please contact our technical support team at support@example.com.

