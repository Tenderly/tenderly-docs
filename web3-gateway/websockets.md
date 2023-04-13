---
description: >-
  Tenderly WebSockets offer a faster method of accessing Ethereum's JSON-RPC and
  provide developers with a more stable and persistent connection to the
  Gateway.
---

# WebSockets

## What are WebSockets?

WebSockets are a communication protocol that allows for real-time, bidirectional, and full-duplex communication between a client and a server. Unlike traditional HTTP requests, which follow a request/response model, WebSockets enable both the client and server to send messages to each other independently, without the need for a new request from the client every time.

## How do WebSockets differ from HTTP?

WebSockets provide several benefits over traditional HTTP requests, such as:

* **Real-time data:** WebSockets allow for real-time data transfer, where updates can be sent to the client as soon as they become available, without requiring the client to make a new request.
* **Lower latency:** Because WebSockets establish a persistent connection between the client and server, there is less overhead and latency than with traditional HTTP requests.
* **Lower server load:** Because WebSockets allow for a persistent connection, the server can send updates to multiple clients without having to send the same data to each client individually.

## How to connect to Tenderly WebSocket?

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Web3 Gateways Page</p></figcaption></figure>

You can go to your [Tenderly Dashboard](https://dashboard.tenderly.co/?redirectTo=gateways) and click on **Copy WSS URL** button. One way to test Tenderly WebSockets is to use the command-line tool `wscat`. Here's an example of connecting to a Tenderly WebSocket:

```bash
wscat -c wss://mainnet.gateway.tenderly.co/$TENDERLY_GATEWAY_ACCESS_TOKEN
```

Replace **TENDERLY\_GATEWAY\_ACCESS\_TOKEN** with the token of your Tenderly Gateway for your project.

Once connected, you can send JSON-RPC requests to the Tenderly WebSocket, and you will receive responses in real time. For example, you can try sending a **eth\_blockNumber** request:

```bash
{"jsonrpc":"2.0","id":1,"method":"eth_blockNumber","params":[]}
```

You should receive a response that looks something like this:

```bash
{"jsonrpc":"2.0","id":1,"result":"0x657330"}
```
