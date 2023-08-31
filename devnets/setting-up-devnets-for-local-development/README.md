---
description: Learn how to use DevNets as part of your local development workflows.
---

# Setting Up DevNets for Local Development

In this guide, you'll learn how to set up DevNets for local development in a HardHat, Foundry, and Truffle project.&#x20;

{% embed url="https://www.youtube.com/watch?v=wIdodbXV6GA" %}

### Why use DevNets in your local development workflows?

1. **Faster development and testing**: Quickly test and debug smart contracts without the latency of public testnets or Mainnet and accelerate your development and debugging.
2. **Customization of the network state**: You get full control over the network, including the state, block number, account balances, timestamp, etc. This allows you to customize the environment to match your project requirements.
3. **Privacy and security**: Your smart contracts and sensitive data remain private during development and testing. This can be particularly important if you are working on proprietary projects or handling sensitive user data that should not be exposed on public networks.
4. **Independence from public testnets**: Acquiring ETH on testnets can be a tedious and time-consuming process, often requiring you to use faucets or request tokens from others. DevNet eliminates this issue by providing a seamless way to add funds to your account. Additionally, it allows for faster transaction execution, enabling you to test and iterate on your smart contracts more efficiently.
5. **Integration with development tools**: A local DevNet is integrated with Tenderly's development toolset, such as Debugger and Gas Profiler. Seamless integration can streamline your development workflow, enabling you to work more efficiently and boost productivity.

### Prerequisites

Before setting up a DevNet locally, ensure you have completed the following steps:

1. **Create a Tenderly account:** If you haven't already, [sign up for Tenderly to access DevNets](https://dashboard.tenderly.co/register?redirectTo=devnets).
2. **Set up a DevNet template:** After creating your account, configure a DevNet Template to match your project's requirements.

{% hint style="info" %}
If you haven't completed these steps, please visit this page for guidance on [creating a DevNet template](../intro-to-devnets.md#basic-devnet-usage).&#x20;
{% endhint %}

{% content-ref url="devnets-with-hardhat.md" %}
[devnets-with-hardhat.md](devnets-with-hardhat.md)
{% endcontent-ref %}

{% content-ref url="devnets-with-foundry.md" %}
[devnets-with-foundry.md](devnets-with-foundry.md)
{% endcontent-ref %}

{% content-ref url="devnets-with-truffle.md" %}
[devnets-with-truffle.md](devnets-with-truffle.md)
{% endcontent-ref %}
