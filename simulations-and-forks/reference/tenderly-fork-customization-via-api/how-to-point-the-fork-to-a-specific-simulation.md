---
description: >-
  Learn how to reset transactions on your Fork by referencing the simulation
  used as a basis for new simulations.
---

# How to Point the Fork to a Specific Simulation

### Updating the fork: Timemachine

At some point, you may want to reset your Fork and discard all transactions and state changes resulting from your simulations. You can do this by updating the “head” of the Fork. The head is a reference to a simulation on top of which new simulations are done. Effectively, it points to the last executed simulation.

In this example, we’ll move where the head points, so we’re literally “removing” or “forgetting” transactions that happened since that particular simulation. In other words, we’re going back in time:

**API Typescript**

```tsx
const req = {
  fork_head: respTxApprove.simulation.ID
}

const fork = await axios.put(tenderlyAPI, "fork", req)
```

### Moving the Fork using JSON-RPC

If you’re doing transactions on Tenderly by connecting your Web3 provider (ethers.js) to a Tenderly JSON-RPC provider, you can achieve the same by invoking `evm_snapshot` and `evm_reset:`

```tsx
contract.send(...) // 1
contract.send(...) // 2
// get an ID of last transaction, think git tag
const checkpoint = provider.send("evm_snapshot", []);

contract.send(...) // 3
contract.send(...) // 4

// revert back the checkpoint
provider.send("evm_revert", [checkpoint]);

// head becomes 2
```
