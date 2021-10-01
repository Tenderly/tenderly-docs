# Gas Profiler

![](../../../.gitbook/assets/image%20%2854%29.png)

The chart you see in the image above is called a flame graph. It is a common way to show usage of a resource like a CPU. The example above is a Kyber Network transaction, [which you can find here](https://dashboard.tenderly.co/tx/main/0x97c37f37988c010a37a8c550b03af37c04bffa2ba6be7d1135f0a26c0e00f532/gas-usage?utm_source=blog&utm_medium=post&utm_campaign=10_ways&utm_content=kyber_network).

Each line shows the sum cost of the lines beneath it. If you click on any of the lines \(functions\), you can see a detailed breakdown of the gas cost of the functions that were invoked.

![](../../../.gitbook/assets/image%20%2842%29.png)

You can finally see which functions are using the most gas and pick the right parts of your code to optimize.

