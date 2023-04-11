# Investigating a Hack (Cover Protocol)

This example will showcase briefly how the all-in-one Tenderly platform can be used to analyze and even prevent hacks such as what happened with the [Cover Protocol](https://twitter.com/CoverProtocol).

The Cover Protocol got hacked because of the inability of code to update the cache in storage. This could have potentially been prevented by using an [**setting up alerts on important functions**](broken-reference) like deposit/withdrawal and particular state changes to prevent an attack.&#x20;

In order to manually analyze the hack, we need to [**import the smart contract**](../../monitoring/smart-contracts/) `Blacksmith` in which the vulnerability was found. If you know the exact name of the affected protocol or vulnerable contract you can also search for it directly.

![](https://lh3.googleusercontent.com/BVJobjB-JHrSGyTHuC7v3cPLBbaUnNJH3pda8uJrHU2qCSV6ms-84BC614vdozpemjg5FO8J4cu-B9RjTTLfYWRQyBneYVBbLy5fv5\_OQA1N-svrza9ZF6Q6xsUA5o37YyYPnaP4)

{% hint style="warning" %}
Note - you can only search for contracts which have been publicly verified on Tenderly or Etherscan. [**Read more about how to verify a contract on Tenderly right here.**](../../monitoring/smart-contract-verification/verifying-a-smart-contract.md)
{% endhint %}

If the contract is not publicly verified, you can do it yourself in order to be able to use it with Tenderly. If the project is open-source (like Cover), you can go to the project's [GitHub repo](https://github.com/CoverProtocol/cover-token-mining), find the contract you want to use (and its source code) and verify it yourself.

![](https://lh4.googleusercontent.com/vWVW6dAj1J6d83juyoXZ3cR9DTMmVgXu9PYHUUL4\_Mv5LRAJ8wnXSckv72tEv-C96zOeutweZaLAx4OEaVBon1PkZOGMBmPwKLlTBJuPEAaPkZSDjwwtip3Kzx1d8B-UzYA7wRkE)

![](https://lh4.googleusercontent.com/C6BHcXHp8NHQmkb7kJP2vwNDi86mVgb-GyHb5Fp9OtddF3anpTTCdkERiNXAGYXnuhippPJKPuxf6a9RW1GIu91nECQWoV033C7gg1GHnz5tsoEP3BkkcMMiAHDCUspbmMz-BVUf)

Now that we have the contract we want to import to Tenderly, go to your Dashboard and click on the **Contracts** tab on the left, and then on the **Add Contract** button in the top right:

![](<../../.gitbook/assets/Screenshot 2021-12-01 at 10.28.37.png>)

You can either upload and verify the contract's code through your Dashboard, or via the CLI [\[more info here\]](../../monitoring/smart-contract-verification/verifying-a-smart-contract.md):

![](<../../.gitbook/assets/Screenshot 2021-12-01 at 10.30.25.png>)

![](<../../.gitbook/assets/Screenshot 2021-12-01 at 10.30.30.png>)

Now, after importing and verifying the contract let us analyze the hack itself. We know that the bug existed in the deposit function's cache so we will simulate that function. As we can see on the screenshot below, after execution it failed with the `Blacksmith: pool does not exist`.

![](https://lh5.googleusercontent.com/JlFsuawkRAxjCnd7sHefFA9n-WpUOPMWIlnXb\_IBOrdvQI8OFvRvTsWPH02p9qy1tmqDf8HnwVgJM2hK3x2iAmvWXNLj-qNLqDzyUmBBG4nbRAmkjfkpRGkh8748cFr052jEoaBL)

Now, let's open this error in [**Tenderly Debugger**](./). On line 118 we see `Pool memory pool = pools[_lpToken];` in the deposit function where data is cached, and later updated on line 125 where we see `_claimCoverRewards(pool, miner);`&#x20;

The contract used the cache data because the data itself stayed in memory; that’s why later the contract calculated the function using that data. Cache was not updated which resulted in this hack:

`miner.rewardWriteoff = miner.amount.mul(pool.accRewardsPerToken).div(CAL_MULTIPLIER);`&#x20;

`miner.bonusWriteoff = miner.amount.mul(bonusToken.accBonusPerToken).div(CAL_MULTIPLIER);`

![](https://lh3.googleusercontent.com/6jPAgWs9ZLNkM7PzW\_g-0kR0Wy5kYMtk80huWk\_KzsfpF7WBTrhE3VIWvPTI0bwVQmR25TLsARV-Ea3f2mK\_kwcYESQEjxKebHv19YbNEuG-Jr0MJQ4t\_LsxV-Q83rB\_SC1NGV1v)

```
function deposit(address _lpToken, uint256 _amount) external override {

require(block.timestamp >= START_TIME , "Blacksmith: not started");

require(_amount > 0, "Blacksmith: amount is 0");

Pool memory pool = pools[_lpToken];

require(pool.lastUpdatedAt > 0, "Blacksmith: pool does not exists");

require(IERC20(_lpToken).balanceOf(msg.sender) >= _amount, "Blacksmith: insufficient balance");

updatePool(_lpToken);



Miner storage miner = miners[_lpToken][msg.sender];

BonusToken memory bonusToken = bonusTokens[_lpToken];

_claimCoverRewards(pool, miner);

_claimBonus(bonusToken, miner);



miner.amount = miner.amount.add(_amount);

// update writeoff to match current acc rewards/bonus per token

miner.rewardWriteoff = miner.amount.mul(pool.accRewardsPerToken).div(CAL_MULTIPLIER);

miner.bonusWriteoff = miner.amount.mul(bonusToken.accBonusPerToken).div(CAL_MULTIPLIER);



IERC20(_lpToken).safeTransferFrom(msg.sender, address(this), _amount);

emit Deposit(msg.sender, _lpToken, _amount);


}
```

* A new pool was approved for liquidity mining, merely hours before the hack. This pool is perfectly normal but since it was new, the blacksmith contract didn’t have any LP token of this pool.
* The attacker deposited some tokens of this pool into the Blacksmith contract.
* The Blacksmith contract keeps track of rewards on a per-token basis. If a lot of tokens are locked, the per-token reward will be small. If very few tokens are locked, the per-token reward will be large. The relevant variable is called `accRewardsPerToken` and is calculated as `totalPoolRewards / totalTokenBalance`.
* The attacker then withdrew almost all of the LP tokens from the Blacksmith contract, reducing the `totalTokenBalance` amount to almost zero.
* The attacker then deposited some tokens of this pool again into the Blacksmith contract. This is where the bug showed its true colors. Since the `totalTokenBalance` was reduced a lot in the previous transaction, the newly calculated `accRewardsPerToken` shot up. The contract uses `rewardWriteoff` to keep the effect of `accRewardsPerToken` in check. However, due to the bug, the old (small) value of `accRewardsPerToken` was used when calculating the `rewardWriteoff` value. Due to this, the large value of `accRewardsPerToken` remained unchecked.
* The attacker then withdrew their rewards. Since there was a large, unchecked value in `accRewardsPerToken`, the total reward paid out of the system got inflated and the **contract ended up minting 40,796,131,214,802,500,000 COVER tokens**.

{% hint style="info" %}
Thanks to Mudit Gupta for the last part of this hack breakdown - [read more about it on his blog](https://mudit.blog/cover-protocol-hack-analysis-tokens-minted-exploit/) :)
{% endhint %}
