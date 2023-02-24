# Deploy smart contracts once per test-suite execution

You may want to deploy your smart contract once per test suite, and have all your test methods (`it`s) use that very instance. This is particularly important if you have large number of tests and smart contracts to deploy where the time complexity is $$O(N_TN_{SC})$$.

To achieve this we’ll just do a Fork at the level of test-suite (`before`). Think of it as a Fork dedicated to deploy contracts for your test suite.

{% hint style="warning" %}
Note that isolation of tests is not available in this setup. Any modification to the contract’s state made in execution of one test will be visible to other tests within the suite. One way to overcome this is to [reset test transactions after completion](reset-transactions-after-completing-the-test.md).
{% endhint %}

The second test (`Should see initially specified message`) shows that whatever is left behind first test in terms of contract state will be visible to the second test (message in french, not the initial message):

```tsx
describe("Deploy before tests without isolation", function () {
    let greeter: Greeter;
    let fork: EthersOnTenderlyFork;

    before(("Deploy contract once"), async () => {
        const forkAndContract = await forkAndDeployGreeter()
        greeter = forkAndContract.greeter;
        fork = forkAndContract.fork;
    });

    it("Should change the greeting message", async () => {
        await (
            await greeter
                .connect(fork.signers[2])
                .setGreeting("Bonjour le monde!")
        ).wait();

        expect(await greeter.greet()).to.equal("Bonjour le monde!");
    })

    it("Should see message specified by the last executed test", async () => {
        expect(await greeter.greet()).to.equal("Bonjour le monde!");
    });

    it("Should fail if non-owner resets greeting", async () => {
        try {
            await greeter
                .connect(fork.signers[2])
                .resetGreeting()
            fail("Should have been a failed transaction")
            // fixme: this should be a different message (specified in SOL)
        } catch (e) {
            console.error("OK, went wrong");
        }
    })
});
```
