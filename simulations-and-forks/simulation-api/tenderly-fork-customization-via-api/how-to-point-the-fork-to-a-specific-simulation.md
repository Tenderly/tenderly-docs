# How to Point the Fork to a Specific Simulation

### Updating the fork - Timemachine

At some point, you may want to reset the Fork and discard all transactions and state changes incurred from your simulations. We can do this by updating the “head” of the Fork. The head is a reference to a Simulation on top of which new Simulations are done. Effectively, it points to the last executed Simulation.

In this example, we’ll move where the head points, so we’re literally “removing” or “forgetting” transactions that had happened since that particular Simulation. In other words, we’re going back in time:

**API Typescript**

```tsx
const req = {
  fork_head: respTxApprove.simulation.ID
}

const fork = await axios.put(tenderlyAPI, "fork", req)
```

### Moving the fork using JSON-RPC

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
