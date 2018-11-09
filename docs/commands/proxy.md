# Tenderly Proxy

Proxy command create a proxy server that forwards all of your request to ethereum rpc node. 

Eth_getTransactionReceipt request will check if transaction failed and print stacktrace in status field 

### Usage:
    tenderly proxy
    
### Command flags:
    --target-schema     Blockchain rpc server schema      (default: http)
    --target-host       Blockchain rpc server host        (default: 127.0.0.1)
    --target-port       Blockchain rpc server port        (default: 8545)
    --proxy-host        Server host                       (default: 127.0.0.1)
    --proxy-port        Server port                       (default: 9545)
    --path              Path to the project build folder  (default: .)
