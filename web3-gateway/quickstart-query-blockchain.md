---
description: >-
  Learn  how to obtain Web3 Gateway JSON RPC access link and how to quickly query the blockchain data from your browser.
---

# Quickstart: querying blockchain data

This how-to guide will guide you through using Web3 Gateway to query the Mainnet for the latest block number.

## Query Mainnet's latest block number

On the left side-menu click **Web3 Gateway**. This will open the Web3 Gateway page, presenting the list of networks and Request builder.

![Web3 Gateway landing page with list of networks](../.gitbook/assets/gw-networks-01.png)

Below the list of networks, you'll find the request builder.

**Step 1:** From the first drop-down menu, select Mainnet.
**Step 2:** From the second dropdown, select **eth_blockNumber**. This JSON RPC method will return the latest block number on the network.

![Setting up eth_blockNumber call on Mainnet](./../.gitbook/assets/gw-call-01-setup.png)

**Step 3**: Click **Send Request**.
The result with the latest block number will show up in the lower pane. Results are shown in JSON RPC response format.

![Examining the raw response](./../.gitbook/assets/gw-call-02-response-raw.png)

**Step 4**: Click the **Decoded** tab to see results in a more accessible form:

![Examining the decoded response](./../.gitbook/assets/gw-call-03-response-decoded.png)

**Step 5**: In the **Request Preview** click **cURL** and click **Copy**.
The cURL calling the **eth_blockNumber** will be in your clipboard.

![Copying the cURL request](./../.gitbook/assets/gw-call-04-curl-copy.png)

**Step 6:** Open a terminal, paste the command, and hit Enter.
You just interacted with blockchain from your command line!

Output should be similar to the previous one:

![Running the cURL request](./../.gitbook/assets/gw-call-05-curl-terminal.png)
