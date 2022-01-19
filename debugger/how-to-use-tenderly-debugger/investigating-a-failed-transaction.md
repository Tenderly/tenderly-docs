# Investigating a Failed Transaction

In this example we will showcase how to investigate a failed transaction on the example of [**Furucombo**](https://furucombo.app) - a platform for easy optimization of DeFi investment strategies.&#x20;

By visualizing complex DeFi protocols as cubes and allowing the user to define the inputs and outputs, Furucombo is able to bundle all of the user transactions i.e. cubes into one and send it out.&#x20;

Because the transactions are bundled in this way, it is even more important to be able to see what happened in each and every step and solve issues quickly.



### Example 1

#### Transaction Intro

The user wanted to repay the DAI debt on AAVE, but only had WMATIC at hand - check out the [Decombo breakdown here](https://furucombo.app/decombo?chainId=137\&txHash=0xbcd377e337ce8e9fc391888a8bb95883923e4385fa548fe230ef0b7c8c56e578) to see what actions does this transaction include.

![](https://lh4.googleusercontent.com/ah\_vAF4pSa0M60hGLLgTpcFTauo7c0XDi6BSHHjgG0vdZIiFoLA05XtLf8lxOMbBy55c0Phl2A94R3lk2fVaESRENY-Hr1ercrEgnDvfBh3zoBj2e6-1VAh9Zb1rCd86mLkXhZ3W)

#### Investigating with Tenderly

By searching the transaction hash on Tenderly we can see everything that happened with it, as well as deep dive in order to find the breaking point:

![](<../../.gitbook/assets/Screenshot 2021-11-08 at 13.24.09.png>)

The [transaction failed](https://dashboard.tenderly.co/tx/polygon/0xbcd377e337ce8e9fc391888a8bb95883923e4385fa548fe230ef0b7c8c56e578) at the `repay` step (screenshots below), as the repay amount should've been 180.80 DAI, but there is [only 180.6658 DAI available](https://dashboard.tenderly.co/tx/polygon/0xbcd377e337ce8e9fc391888a8bb95883923e4385fa548fe230ef0b7c8c56e578/debugger?trace=0.12.2.1.2.0.2.0.8.0.1.1.0.0.1) after the swap in the first step.

![](https://lh3.googleusercontent.com/Sb1XyfSiZ5Kv9GnQdpiLaQ2s7Bt3VDWBYdpf9ntSbNHng\_7uQOmL-SGChYHDOy8ne7C6vw1gO1kuaLU4jytWf0kDD91ckYHsVtAlkc0QTf7odVr4GS-idS\_Mf0EF4bcAuwF0bRY1)

![](https://lh4.googleusercontent.com/g7cQNIrA\_wCPclSEqaLusyipNrVu4-XoBXop5M2uNFb8MeLBTvxlKcZoQfbtn1IsYZ5SxhYcJ0P5f9GG6\_4ex2KNHAHvV9wCln2IN7ytaDmHe\_GTbB5Iy-C2or0hZm2Wc7WgWpoX)

#### Solution

As a way to avoid these issues in the future, we could lower the amount between `swap` and `repay` steps to allow for price slippage (\~0.3%). Alternatively, by using the `previous output` feature when inputing the amount for the second cube we will ensure sending the exact and expected amount from the first cube.

{% hint style="success" %}
You can **comment and prioritize any trace you want**, either for yourself or to make collaboration in the project easier. You can [**read more about it here**](../../monitoring/contracts/commenting-and-prioritizing-traces.md).
{% endhint %}

### Example 2

#### Transaction Intro

A user wanted to move liquidity between different pools, as seen in [this Decombo link](https://furucombo.app/decombo?chainId=137\&txHash=0xafa72ac178ba6e67b5b580082130b91ac64421941d6cf72c0d518fe6b8977106):

![](https://lh4.googleusercontent.com/wWQGWGPQyTozSja6pdVfC3taTde9JCNnrwFaCRjs1OQmtMIRIsyoFL2NhhbBaykTlVLRYzlT7CHXsp6kiJBzU\_4Vm1zu1FbwTochARKuigWe4iMPW8GfMZONOIEvNd6OH4-l50lT)

#### Investigating with Tenderly

The [transaction failed](https://dashboard.tenderly.co/tx/polygon/0xafa72ac178ba6e67b5b580082130b91ac64421941d6cf72c0d518fe6b8977106) at the `check slippage` step, which is the final step when executing a Furucombo transaction.

![](https://lh6.googleusercontent.com/A3crA2U-sqGnWvobqeWBP6C70QDY3QejK2dHIDblApHVcsXcYjY3qoEnnwahJ6EQdue6QN7wG4dL7SLKI8xqxFWs7saEvPf0eCuV5wKw\_8qO56\_QcxcVxdaDtbPaLa2UISye9sZD)

[Looking at the slippage tolerance](https://dashboard.tenderly.co/tx/polygon/0xafa72ac178ba6e67b5b580082130b91ac64421941d6cf72c0d518fe6b8977106/debugger?trace=0.0.0.8.1.3.27.2) numbers, it seems it is required to have 6.439851 USDC:

![](https://lh3.googleusercontent.com/YLchfzl5OZuxEyLAOIo5yzbTb\_coPT2odDkXScWKZ4GpxRemHypme1akWzeG5IuoAFh\_OzqEpaPgbDuXN2288yfIhyzlOJuVGKBuMiFpWLg9-aAqIotxEeVn38NdNGFMBeZ9NsAP)

Turns out that [only 3.999420 USDC are left](https://dashboard.tenderly.co/tx/polygon/0xafa72ac178ba6e67b5b580082130b91ac64421941d6cf72c0d518fe6b8977106/debugger?trace=0.0.0.8.1.3.27.2.1.0), which is lower than the slippage tolerance:

![](https://lh3.googleusercontent.com/EUXHTnFr9N4yE\_GbjxXy-KJxGEOXODGYNCCJl0MsyXnbAULj8LZNlOszBHxpftgi7cvjk2OZGBUYlZ5m-X2utt4QqqbRvjAO0A9NykuvE\_-eR97ZVaO65\_JtWV1QRl8sZHZCL-S-)

#### Solution

Lowering the amount between steps in order to allow for price slippage (\~0.3%) when the `previous output` feature is not applicable.
