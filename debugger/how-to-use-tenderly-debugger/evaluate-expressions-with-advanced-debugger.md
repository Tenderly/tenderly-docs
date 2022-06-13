---
description: Trace Eval
---

# Evaluate Expressions with Advanced Debugger

{% hint style="success" %}
We wrote a blog explaining in more detail what Evaluate Expression is and how it came to be, how and why you should use it, as well as some common use cases to get you started, such as:

* #### Evaluating complex expressions <a href="#1-evaluating-complex-expressions" id="1-evaluating-complex-expressions"></a>
* **Evaluating dynamic arrays, mappings, and other state variables**
* **Evaluating functions**
* **Evaluating global and local variables**

****\
****You can read more about it right here :point\_down:
{% endhint %}

{% embed url="https://blog.tenderly.co/how-use-evaluate-expression-speed-debugging/" %}

You can now evaluate expressions in the execution trace! Go to any transaction in the "Transactions" in the left-hand navigation, then go to the "Debugger" tab, and click on the "Evaluate" button:

![](<../../.gitbook/assets/Screenshot 2022-04-14 at 12.33.34.png>)

![](<../../.gitbook/assets/Screenshot 2022-04-14 at 12.34.54.png>)

![](<../../.gitbook/assets/Screenshot 2022-04-14 at 12.36.18.png>)

The Eval feature is currently only supported for Solidity contracts, and we're working on supporting Eval for Vyper contracts as well. Choose any expression you want to evaluate, paste it into the box and hit the `Evaluate` button:

![](<../../.gitbook/assets/Screenshot 2022-04-14 at 12.44.01.png>)

![](<../../.gitbook/assets/Screenshot 2022-04-14 at 12.44.36.png>)

![](<../../.gitbook/assets/Screenshot 2022-04-14 at 12.44.57.png>)

This works for both simple and complex expressions:

![](<../../.gitbook/assets/Screenshot 2022-04-14 at 12.45.55.png>)

![](<../../.gitbook/assets/Screenshot 2022-04-14 at 12.47.27.png>)

You can read more about **other Debugger features and Advanced Trace Search** [**here**](https://docs.tenderly.co/debugger/how-to-use-tenderly-debugger#stack-traces) **and** [**here**](https://docs.tenderly.co/monitoring/contracts#advanced-trace-search).
