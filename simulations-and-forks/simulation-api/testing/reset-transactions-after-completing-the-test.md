# Reset transactions after completing the test

To address the isolation issue, we can use a custom JSON RPC: `evm_snapshot` to create a snapshot to the point before the actual test execution (`beforeEach`). This call gives us an ID of the snapshot (stored in `snap`). You can think of it as a pointer to a particular point on the chain.

After the test is complete (in `afterEach`), we invoke the `evm_revert` and pass it to the snapshot ID:

```jsx
import { fail } from "assert";
import { expect } from "chai";
import { Greeter } from "../typechain";
import { forkAndDeployGreeter } from "./utils";
import { EthersOnTenderlyFork } from "./utils/tenderly/fork";

describe("Deploy before tests forget execution", function () {
    let greeter: Greeter;
    let fork: EthersOnTenderlyFork;
    let snap: null | string = null;

    before(("Deploy contract once"), async () => {
        const forkAndContract = await forkAndDeployGreeter()
        greeter = forkAndContract.greeter;
        fork = forkAndContract.fork;
    });

    beforeEach(async () => {
        snap = await fork.provider.send("evm_snapshot", []);

    })

    afterEach(async () => {
        await fork.provider.send("evm_revert", [snap]);
    })

    it("Should change the greeting message", async () => {
        await (
            await greeter
                .connect(fork.signers[2])
                .setGreeting("Bonjour le monde!")
        ).wait();

        expect(await greeter.greet()).to.equal("Bonjour le monde!");
    })

    it("Should see message specified by the last executed test", async () => {
        expect(await greeter.greet()).to.equal("Hello, world!");
    });
});
```

