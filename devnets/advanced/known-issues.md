---
description: >-
  This page contains a list of known issues in DevNets that we are working to
  address and mitigate.
---

# Known Issues

{% hint style="info" %}
If you encounter any issues not mentioned here, please contact our support team via the chat in the Dashboard or at [support@tenderly.co](mailto:support@tenderly.co). We appreciate your feedback, even for issues listed here.
{% endhint %}

### **Waffle is currently not supported**

We are working on supporting Waffle in the future. In the meantime, try using plain Ethers.

### **`hardhat-network-helpers` is not supported**

If your tests rely on this library, they will most likely fail because it expects the underlying network to be HardHat. We are working to expose this functionality for DevNets as well.

### **Typed errors and reverts are currently not supported**

Development nodes currently handle typed errors, while DevNets do not. This can cause some tests to fail if they rely on newer versions of Solidity.

### **Timeouts**

Due to the hosted nature of DevNets and the framework of the underlying RPC calls (e.g., sending a transaction in Ethers actually involves 13 RPC calls), more complex test suites can experience timeouts.

### **Missing custom RPC calls**

We currently do not support every custom RPC call that other development nodes offer. This can cause some tests that rely on these calls to fail.

Check out the list of all supported [**custom RPC methods**](custom-rpc-methods.md) in DevNets**.**

### **Bad Request Error**

There are several causes for bad request errors:

* Your input parameters do not match the Ethereum JSON RPC protocol. In that case, you will see the error message `invalid params.`
* Your RPC URL is not properly copied from the Dashboard or CLI. The error message will advise you to double-check the RPC URL.
* If everything above is fine, and you still get the error, it is probably because the DevNet has expired. The error message will advise you to double-check if the DevNet is still running in the Dashboard.
