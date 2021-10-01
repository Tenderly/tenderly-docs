# Docker

This document describes how to run your own Tenderly agent which will ship transactions to the Tenderly platform for processing.

The prerequisites for this process is a newer version of Docker and running your own Ethereum node.

## How to install

### Pulling the image

The Tenderly agent images are hosted on our Docker registry which is publicly available.

To pull the image simply run:

```text
docker pull gcr.io/tenderly-public/tenderly-agent:latest
```

This will pull the latest version of the Tenderly agent to your local Docker environment.

### Configuring the agent

The agent is highly customizable when it comes to networking and chain configuration. The configuration itself is done via a simple `yaml` file.

In addition to networking and chain configuration, you can also add certificates for extra security when authenticating with the platform.

The configuration file can be stored anywhere on your system, but we suggest using a file structure along the lines of: `~/tenderly/config/config.yaml`.

### Example configuration file

```text
agent:
  database_path: .db
  networks:
    1582818248889:
      name: private-network
      address: 0.0.0.0:8555
			# the address and port of your local node
			# note: this is the address from the perspective of the container
      rpc_server: 127.0.0.1:8545
      node_type: geth
      chain_config:
        chainId: 1582818248889
        homesteadBlock: 0
        eip150Block: 0
        eip155Block: 0
        eip158Block: 0
        byzantiumBlock: 0
        constantinopleBlock: 0
        petersburgBlock: 0
        istanbulBlock: 0
        clique:
          period: 1
          epoch: 30000
      cert_file: ./.tenderly/cert/testnet.crt # optional
      key_file: ./.tenderly/private/testnet.key # optional
```

### Running the agent

Once you've configured your Tenderly agent you can run it with the following command \(assuming that the configuration file is located at `$(pwd)/tenderly/config/config.yaml`\):

```text
docker run -v $(pwd):/tenderly/config gcr.io/tenderly-public/tenderly-agent
```

Once the agent starts working it will start outputting information for each block that is processed:

![](../../.gitbook/assets/image%20%2868%29.png)

### Connecting the agent with the platform

Once the agent is fully operational, contact the team either via Telegram or [Email](mailto:support@tenderly.dev).

After we authenticate the agent with the platform, you can start pushing your contracts to Tenderly.

[Tenderly CLI](https://github.com/tenderly/tenderly-cli#push)

