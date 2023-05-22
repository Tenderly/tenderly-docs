# DevNets with Foundry

### Setting up DevNet for a Foundry **project**

Foundry is a Rust-based Ethereum smart contract development framework that provides an easy-to-use CLI for developers.

Make sure you have everything installed first:

* [Install Rust](https://www.rust-lang.org/tools/install)
* [Install Foundry](https://github.com/gakonst/foundry/)

To set up a DevNet with Foundry, follow these steps:

1. Initialize a dummy Foundry project.

```bash
forge init
```

2. Use the `forge create` command to deploy your smart contracts.

```bash
forge create --rpc-url=$(tenderly devnet spawn-rpc --template <YOUR_TEMPALATE_SLUG> --project <YOUR_PROJECT_SLUG>) ./src/Counter.sol:Counter --unlocked --from 0x0000000000000000000000000000000000000000
```
