# How to use Tenderly Debugger

The Visual Debugger is one of the tools people love the most. Instead of wasting countless hours debugging transactions, you can use the Visual Debugger so you can focus more on buidling and less on scratching your head.

**The level of detail present here doesn't exist anywhere else and reduces development time by orders of magnitude**.

![](<../../.gitbook/assets/Screenshot 2021-12-22 at 10.55.18.png>)

Go to the **Transactions** tab in the left navigation bar and click on a transaction from the list, or paste the transaction hash you want into the top **Explorer** bar:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.14.57.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.15.58.png>)

By clicking on **Contracts** (or **Addresses**) on the left we can see all of the contracts that have been involved in this transaction:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.17.52.png>)

When you click on the **Debugger** tab, you will see the following:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.26.51.png>)

On the top right you will see the code that was executed, below are the listed parameters for code execution and inputs that were passed into the function, and on the left we have the **Execution** and **Stack Traces**.

### Execution Trace

Execution Trace has two modes you can use - Function Trace and Call Trace.

By default it is set to **Function Trace**, which means it will show all external and internal calls that happened in this transaction.&#x20;

![](<../../.gitbook/assets/Screenshot 2021-12-22 at 10.46.31.png>)

![](<../../.gitbook/assets/Screenshot 2021-12-22 at 10.51.00.png>)

For a better overview of key calls you can switch it to **Call Trace**, which shows only external calls that happened in the transaction.

![](<../../.gitbook/assets/Screenshot 2021-12-22 at 10.47.25.png>)

![](<../../.gitbook/assets/Screenshot 2021-12-22 at 10.51.17.png>)

Now let's take one function and break it down further:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.28.19.png>)

For example the function `multicall` has a single input labeled `data` which is shown below:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.29.15.png>)

On the left you will see a list of all the function that were called in this transaction which are further broken down in the order of execution in the **Stack Trace**:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.30.15.png>)

You can search for the exact term in the code either by double clicking a word and searching for it using the markup to the right, or by hitting CTRL+F to open up the integrated search bar:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.38.01.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.38.49.png>)

### Stack Traces

While we debug our transaction, the **Stack Trace** will show all of the functions that are being executed in each step:

![](<../../.gitbook/assets/image (69) (1) (1) (1) (1).png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.35.12.png>)

### Decoded Events/Logs

When in **Transaction** overview, **Events** tab will show you all of the events emitted in this transaction, with options to filter them out by _event name_ or _contract/address_:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.19.45.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.20.12.png>)

### Decoded State Changes

**State Changes** allows us to see all of the variables that were changed/updated during the course of the transaction:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.21.17.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.22.19.png>)

### Gas Profiler

**Gas Profiler** shows you the most detailed view of how your transaction spent gas, down to every single function call and the amount of gas spent by it:

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.23.42.png>)

![](<../../.gitbook/assets/Screenshot 2021-10-14 at 14.24.05.png>)
