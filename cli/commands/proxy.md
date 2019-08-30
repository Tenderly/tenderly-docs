# proxy

The tenderly proxy command creates a proxy server that listens and forwards all of your request to an Ethereum RPC node.

Eth\_getTransactionReceipt request will check if transaction failed and print stacktrace in status field

## Usage:

```text
tenderly proxy
```

## Command flags:

```text
--target-schema     Blockchain rpc server schema      (default: http)
--target-host       Blockchain rpc server host        (default: 127.0.0.1)
--target-port       Blockchain rpc server port        (default: 8545)
--proxy-host        Server host                       (default: 127.0.0.1)
--proxy-port        Server port                       (default: 9545)
--path              Path to the project build folder  (default: .)
```

