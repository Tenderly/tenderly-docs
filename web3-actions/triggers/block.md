# Block

Periodic trigger means your action will be invoked when blocks are mined on a network.

```
trigger:
  type: block
  block:
    # For now, network must be chain id.
    # You can specify multiple networks, by providing a list of chain ids
    # instead of a single value. 
    network: 1
    # This action will run on every 100th block. T
    blocks: 100

trigger:
  type: block
  block:
    network:
      - 1  # mainnet
      - 3  # kovan
    blocks: 100
```
