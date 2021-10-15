# Block

Block lets you trigger actions as blocks are mined on the network:

```
trigger:
  type: block
  block:
    network: 1  # mainnet
    blocks: 100

# or you can specify multiple networks
trigger:
  type: block
  block:
    network:
      - 1
      - 3
    blocks: 100
```
