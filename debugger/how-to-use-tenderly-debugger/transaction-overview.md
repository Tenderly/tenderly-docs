# Transaction Overview

We’ll be looking into a transaction of a DEX / Flash Loan arbitrage bot that operates on the Ethereum network. You can see the failed transactions [here on Etherscan: 0xf24ef05bf86444eee80788b19f5cc7b92d1fe9091c69ec217659074b371721b6](https://etherscan.io/tx/0xf24ef05bf86444eee80788b19f5cc7b92d1fe9091c69ec217659074b371721b6).

![](../../.gitbook/assets/image%20%2819%29.png)

If you copy the transaction hash

0xf24ef05bf86444eee80788b19f5cc7b92d1fe9091c69ec217659074b371721b6

and paste it in the Tenderly search box at the top of the interface \(when you’re logged in\), we’ll be able to have much more details \([click here](https://dashboard.tenderly.co/tx/main/0xf24ef05bf86444eee80788b19f5cc7b92d1fe9091c69ec217659074b371721b6)\). The transaction may take time to load as Tenderly replays the transaction at the block it was executed to get all the details needed to show you. As soon as it’s loaded you should see something like this:

![](../../.gitbook/assets/image%20%2817%29.png)

As you can see, Tenderly directly display us the correct reason on why the transaction was reverted:

```text
require(returnAmount >= minReturn, “OneSplit: actual return amount is less than minReturn”);
```

We know that when you call 1inch you need to provide the token you want to swap and the amount, the token you want to get and the minimum amount of return you want want to get and the distribution of DEXs that will be used by the swap. In this case we can conclude that the transaction failed because the amount of token returned by the swap is less than the amount of token the transaction specified.

Fortunately, the debugging tool enable us to go deeper to understand how the transaction went step by step before it failed. Let’s look at the first part of the transaction. It describes every calls to different smart contract that were made during the transaction:

![](../../.gitbook/assets/image%20%2816%29.png)

The first part involves Dy/Dx protocol that can be used as a flash loan platform. We can see that the flash loan has something to do with TetherToken \(USDT\). Then the second part involves a call to the swap function of 1inch DEX aggregator:

![](../../.gitbook/assets/image%20%2812%29.png)

If you overlay a function you’ll have the option to move to the debugger view of the selected state, we have this for the swap function:

![](../../.gitbook/assets/image%20%2833%29.png)

You can see that once the transaction did the flash loan it first tried to swap the tokens using 1inch. The from token is USDT, the toToken is wrapped Ether: WETH. The smart contract asks to swap 4234.575953 USDT to at least 19 Ether. As you can see Tenderly enable us to decode every parameter of internal calls even if the transaction failed. If you’re interacting with known contract the tool will directly decode the parameters for you otherwise you can upload your own smart contracts to the platform. 

If we scroll down enough until the place where the transaction was reverted at the end of the swap call:

![](../../.gitbook/assets/image%20%2842%29.png)

If we go in the debugger view of this call we’ll be able to get details:

![](../../.gitbook/assets/image%20%2811%29.png)

Thanks to the previous/next button you’ll be able to navigate each steps of the transaction and see that the return amount \(one step before\) was - 18.953135705079702716:

![](../../.gitbook/assets/image%20%2813%29.png)

So using Tenderly to debug the transaction we were able to see where and how the transaction failed in few minutes.

