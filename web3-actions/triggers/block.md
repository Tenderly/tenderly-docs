# Block

Block lets you trigger actions as blocks are mined on the network:

```
trigger:
  type: block
  block:
    network: 1  # mainnet
    blocks: 100

trigger:
  type: block
  block:
    network:
      - 1  # mainnet
      - 3  # kovan
    blocks: 100
```
