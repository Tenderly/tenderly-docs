---
description: Custom JSON RPC method available in Tenderly Web3 Gateway
---

# Trace JSON RPC

{% hint style="info" %}
The custom RPC methods appear in the **`tenderly_`** namespace.
{% endhint %}

### `tenderly_traceTransaction`

Replays transaction on the blockchain and provides information about the execution, such as status, logs, internal transactions, etc.

**PARAMS**

1. **Transaction hash** `STRING` 32 byte hex value

{% tabs %}
{% tab title="Raw" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "tenderly_traceTransaction",
  "params": ["0x6b2264fa8e28a641d834482d250080b39cbbf39251344573c7504d6137c4b793" ]
}
```
{% endtab %}

{% tab title="cURL" %}
```bash

curl https://mainnet.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY \
-X POST \
-H "Content-Type: application/json" \
-d \
'{
  "id": 0,
  "jsonrpc": "2.0",
  "method": "tenderly_traceTransaction",
  "params": ["0x6b2264fa8e28a641d834482d250080b39cbbf39251344573c7504d6137c4b793"]
}'

```
{% endtab %}

{% tab title="ethers" %}
```javascript
// Installation Instructions: https://docs.ethers.io/v5/getting-started/#installing
const { ethers } = require("ethers");

async function runSimulateTransaction() {
  // Initialize an ethers instance
  const provider = new ethers.providers.JsonRpcProvider(
    "https://goerli.gateway.tenderly.co/$TENDERLY_WEB3_GATEWAY_KEY"
  );

  // Execute method
  const result = await provider.send("tenderly_traceTransaction", [
    "0x6b2264fa8e28a641d834482d250080b39cbbf39251344573c7504d6137c4b793"
  ]);

  // Print the output to console
  console.log(result);
}

(async () => {
  runSimulateTransaction();
})();
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "id": 0,
  "jsonrpc": "2.0",
  "result": {
    "status": true,
    "gasUsed": "0x2da74",
    "cumulativeGasUsed": "0x0",
    "blockNumber": "0xfbc520",
    "type": "0x0",
    "logsBloom": "0x00200080000000000000000080000000000000000000000000010040000000000000000000000000000000000000000002000000080000000000000000000000000000000000000000000008000000200000000000000008000000008000000000000000000000001000000000000000000000000000800040000010000000000000000000000000004000000000000000000001080000080000004000000000000000000000000000080000000000000000000000000000000200000000000000000002000000000000000000000000004000000000001000010000000020000000200000000000000000200000000000000000000000400000000000000000",
    "logs": [
      {
        "name": "Deposit",
        "anonymous": false,
        "inputs": [
          {
            "value": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
            "type": "address",
            "name": "dst"
          },
          {
            "value": "25000000000000000",
            "type": "uint256",
            "name": "wad"
          }
        ],
        "raw": {
          "address": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
          "topics": [
            "0xe1fffcc4923d04b559f4d29a8bfc6cda04eb5b0d3c460751c2402c5c5cc9109c",
            "0x0000000000000000000000007a250d5630b4cf539739df2c5dacb4c659f2488d"
          ],
          "data": "0x0000000000000000000000000000000000000000000000000058d15e17628000"
        }
      },
      {
        "name": "Transfer",
        "anonymous": false,
        "inputs": [
          {
            "value": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
            "type": "address",
            "name": "src"
          },
          {
            "value": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
            "type": "address",
            "name": "dst"
          },
          {
            "value": "25000000000000000",
            "type": "uint256",
            "name": "wad"
          }
        ],
        "raw": {
          "address": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
          "topics": [
            "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
            "0x0000000000000000000000007a250d5630b4cf539739df2c5dacb4c659f2488d",
            "0x000000000000000000000000a0c9bf9aa601ddfb1cdf3be3ef77e010e4184076"
          ],
          "data": "0x0000000000000000000000000000000000000000000000000058d15e17628000"
        }
      },
      {
        "name": "Transfer",
        "anonymous": false,
        "inputs": [
          {
            "value": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
            "type": "address",
            "name": "from"
          },
          {
            "value": "0x17b11ed010e715bf4336a88489fe4f0ef6a09dc7",
            "type": "address",
            "name": "to"
          },
          {
            "value": "1201840076490568",
            "type": "uint256",
            "name": "value"
          }
        ],
        "raw": {
          "address": "0xd81781e686d0ad128b4c7e7b3c072b89f509ea2a",
          "topics": [
            "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
            "0x000000000000000000000000a0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
            "0x00000000000000000000000017b11ed010e715bf4336a88489fe4f0ef6a09dc7"
          ],
          "data": "0x0000000000000000000000000000000000000000000000000004451132d60748"
        }
      },
      {
        "name": "Sync",
        "anonymous": false,
        "inputs": [
          {
            "value": "5161635883710151874",
            "type": "uint112",
            "name": "reserve0"
          },
          {
            "value": "263488971740003263",
            "type": "uint112",
            "name": "reserve1"
          }
        ],
        "raw": {
          "address": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
          "topics": [
            "0x1c411e9a96e071241c2f21f7726b17ae89e3cab4c78be50e062b03a9fffbbad1"
          ],
          "data": "0x00000000000000000000000000000000000000000000000047a1d07d1c73fcc200000000000000000000000000000000000000000000000003a819d2e2cbbbbf"
        }
      },
      {
        "name": "Swap",
        "anonymous": false,
        "inputs": [
          {
            "value": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
            "type": "address",
            "name": "sender"
          },
          {
            "value": "25000000000000000",
            "type": "uint256",
            "name": "amount0In"
          },
          {
            "value": "0",
            "type": "uint256",
            "name": "amount1In"
          },
          {
            "value": "0",
            "type": "uint256",
            "name": "amount0Out"
          },
          {
            "value": "1278553272862306",
            "type": "uint256",
            "name": "amount1Out"
          },
          {
            "value": "0x17b11ed010e715bf4336a88489fe4f0ef6a09dc7",
            "type": "address",
            "name": "to"
          }
        ],
        "raw": {
          "address": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
          "topics": [
            "0xd78ad95fa46c994b6551d0da85fc275fe613ce37657fb8d5e3d130840159d822",
            "0x0000000000000000000000007a250d5630b4cf539739df2c5dacb4c659f2488d",
            "0x00000000000000000000000017b11ed010e715bf4336a88489fe4f0ef6a09dc7"
          ],
          "data": "0x0000000000000000000000000000000000000000000000000058d15e176280000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000048ad661a7c662"
        }
      }
    ],
    "trace": [
      {
        "type": "CALL",
        "from": "0x17b11ed010e715bf4336a88489fe4f0ef6a09dc7",
        "to": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "gas": "0x35004",
        "gasUsed": "0x2da40",
        "value": "0x58d15e17628000",
        "input": "0xb6f9de950000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008000000000000000000000000017b11ed010e715bf4336a88489fe4f0ef6a09dc70000000000000000000000000000000000000000000000000000000063d41cf70000000000000000000000000000000000000000000000000000000000000002000000000000000000000000c02aaa39b223fe8d0a0e5c4f27ead9083c756cc2000000000000000000000000d81781e686d0ad128b4c7e7b3c072b89f509ea2a",
        "decodedInput": [
          {
            "value": "0",
            "type": "uint256",
            "name": "amountOutMin"
          },
          {
            "value": [
              "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
              "0xd81781e686d0ad128b4c7e7b3c072b89f509ea2a"
            ],
            "type": "address[]",
            "name": "path"
          },
          {
            "value": "0x17b11ed010e715bf4336a88489fe4f0ef6a09dc7",
            "type": "address",
            "name": "to"
          },
          {
            "value": "1674845431",
            "type": "uint256",
            "name": "deadline"
          }
        ],
        "method": "swapExactETHForTokensSupportingFeeOnTransferTokens",
        "output": "0x",
        "subtraces": 7,
        "traceAddress": [
          0
        ]
      },
      {
        "type": "CALL",
        "from": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "gas": "0x31c34",
        "gasUsed": "0x5da6",
        "value": "0x58d15e17628000",
        "input": "0xd0e30db0",
        "output": "0x",
        "subtraces": 0,
        "traceAddress": [
          0,
          0
        ]
      },
      {
        "type": "CALL",
        "from": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "gas": "0x2bb7b",
        "gasUsed": "0x1f7e",
        "value": "0x0",
        "input": "0xa9059cbb000000000000000000000000a0c9bf9aa601ddfb1cdf3be3ef77e010e41840760000000000000000000000000000000000000000000000000058d15e17628000",
        "decodedInput": [
          {
            "value": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
            "type": "address",
            "name": "dst"
          },
          {
            "value": "25000000000000000",
            "type": "uint256",
            "name": "wad"
          }
        ],
        "method": "transfer",
        "output": "0x0000000000000000000000000000000000000000000000000000000000000001",
        "decodedOutput": [
          {
            "value": true,
            "type": "bool",
            "name": ""
          }
        ],
        "subtraces": 0,
        "traceAddress": [
          0,
          1
        ]
      },
      {
        "type": "STATICCALL",
        "from": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "to": "0xd81781e686d0ad128b4c7e7b3c072b89f509ea2a",
        "gas": "0x29100",
        "gasUsed": "0x19fe",
        "input": "0x70a0823100000000000000000000000017b11ed010e715bf4336a88489fe4f0ef6a09dc7",
        "decodedInput": [
          {
            "value": "0x17b11ed010e715bf4336a88489fe4f0ef6a09dc7",
            "type": "address",
            "name": "account"
          }
        ],
        "method": "balanceOf",
        "output": "0x0000000000000000000000000000000000000000000000000000000000000000",
        "decodedOutput": [
          {
            "value": "0",
            "type": "uint256",
            "name": ""
          }
        ],
        "subtraces": 0,
        "traceAddress": [
          0,
          2
        ]
      },
      {
        "type": "STATICCALL",
        "from": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "to": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
        "gas": "0x267d6",
        "gasUsed": "0x9c8",
        "input": "0x0902f1ac",
        "output": "0x0000000000000000000000000000000000000000000000004748ff1f05117cc200000000000000000000000000000000000000000000000003aca4a9447382210000000000000000000000000000000000000000000000000000000063d41a7f",
        "decodedOutput": [
          {
            "value": "5136635883710151874",
            "type": "uint112",
            "name": "_reserve0"
          },
          {
            "value": "264767525012865569",
            "type": "uint112",
            "name": "_reserve1"
          },
          {
            "value": 1674844799,
            "type": "uint32",
            "name": "_blockTimestampLast"
          }
        ],
        "subtraces": 0,
        "traceAddress": [
          0,
          3
        ]
      },
      {
        "type": "STATICCALL",
        "from": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "gas": "0x25c36",
        "gasUsed": "0x216",
        "input": "0x70a08231000000000000000000000000a0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
        "decodedInput": [
          {
            "value": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
            "type": "address",
            "name": ""
          }
        ],
        "method": "balanceOf",
        "output": "0x00000000000000000000000000000000000000000000000047a1d07d1c73fcc2",
        "decodedOutput": [
          {
            "value": "5161635883710151874",
            "type": "uint256",
            "name": ""
          }
        ],
        "subtraces": 0,
        "traceAddress": [
          0,
          4
        ]
      },
      {
        "type": "CALL",
        "from": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "to": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
        "gas": "0x2542c",
        "gasUsed": "0x1daa9",
        "value": "0x0",
        "input": "0x022c0d9f000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000048ad661a7c66200000000000000000000000017b11ed010e715bf4336a88489fe4f0ef6a09dc700000000000000000000000000000000000000000000000000000000000000800000000000000000000000000000000000000000000000000000000000000000",
        "decodedInput": [
          {
            "value": "0",
            "type": "uint256",
            "name": "amount0Out"
          },
          {
            "value": "1278553272862306",
            "type": "uint256",
            "name": "amount1Out"
          },
          {
            "value": "0x17b11ed010e715bf4336a88489fe4f0ef6a09dc7",
            "type": "address",
            "name": "to"
          },
          {
            "value": "0x",
            "type": "bytes",
            "name": "data"
          }
        ],
        "method": "swap",
        "output": "0x",
        "subtraces": 3,
        "traceAddress": [
          0,
          5
        ]
      },
      {
        "type": "CALL",
        "from": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
        "to": "0xd81781e686d0ad128b4c7e7b3c072b89f509ea2a",
        "gas": "0x220ec",
        "gasUsed": "0x153da",
        "value": "0x0",
        "input": "0xa9059cbb00000000000000000000000017b11ed010e715bf4336a88489fe4f0ef6a09dc700000000000000000000000000000000000000000000000000048ad661a7c662",
        "decodedInput": [
          {
            "value": "0x17b11ed010e715bf4336a88489fe4f0ef6a09dc7",
            "type": "address",
            "name": "recipient"
          },
          {
            "value": "1278553272862306",
            "type": "uint256",
            "name": "amount"
          }
        ],
        "method": "transfer",
        "output": "0x0000000000000000000000000000000000000000000000000000000000000001",
        "decodedOutput": [
          {
            "value": true,
            "type": "bool",
            "name": ""
          }
        ],
        "subtraces": 0,
        "traceAddress": [
          0,
          5,
          0
        ]
      },
      {
        "type": "STATICCALL",
        "from": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
        "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "gas": "0xd008",
        "gasUsed": "0x216",
        "input": "0x70a08231000000000000000000000000a0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
        "decodedInput": [
          {
            "value": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
            "type": "address",
            "name": ""
          }
        ],
        "method": "balanceOf",
        "output": "0x00000000000000000000000000000000000000000000000047a1d07d1c73fcc2",
        "decodedOutput": [
          {
            "value": "5161635883710151874",
            "type": "uint256",
            "name": ""
          }
        ],
        "subtraces": 0,
        "traceAddress": [
          0,
          5,
          1
        ]
      },
      {
        "type": "STATICCALL",
        "from": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
        "to": "0xd81781e686d0ad128b4c7e7b3c072b89f509ea2a",
        "gas": "0xcc65",
        "gasUsed": "0xa5e",
        "input": "0x70a08231000000000000000000000000a0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
        "decodedInput": [
          {
            "value": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
            "type": "address",
            "name": "account"
          }
        ],
        "method": "balanceOf",
        "output": "0x00000000000000000000000000000000000000000000000003a819d2e2cbbbbf",
        "decodedOutput": [
          {
            "value": "263488971740003263",
            "type": "uint256",
            "name": ""
          }
        ],
        "subtraces": 0,
        "traceAddress": [
          0,
          5,
          2
        ]
      },
      {
        "type": "STATICCALL",
        "from": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "to": "0xd81781e686d0ad128b4c7e7b3c072b89f509ea2a",
        "gas": "0x7edd",
        "gasUsed": "0xa5e",
        "input": "0x70a0823100000000000000000000000017b11ed010e715bf4336a88489fe4f0ef6a09dc7",
        "decodedInput": [
          {
            "value": "0x17b11ed010e715bf4336a88489fe4f0ef6a09dc7",
            "type": "address",
            "name": "account"
          }
        ],
        "method": "balanceOf",
        "output": "0x0000000000000000000000000000000000000000000000000004451132d60748",
        "decodedOutput": [
          {
            "value": "1201840076490568",
            "type": "uint256",
            "name": ""
          }
        ],
        "subtraces": 0,
        "traceAddress": [
          0,
          6
        ]
      }
    ],
    "assetChanges": [
      {
        "assetInfo": {
          "standard": "ERC20",
          "type": "Fungible",
          "contractAddress": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
          "symbol": "weth",
          "name": "WETH",
          "logo": "https://assets.coingecko.com/coins/images/2518/large/weth.png?1628852295",
          "decimals": 18,
          "dollarValue": "1834.6199951171875"
        },
        "type": "Mint",
        "to": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "rawAmount": "0x58d15e17628000",
        "amount": "0.025",
        "dollarValue": "45.8654998779296875"
      },
      {
        "assetInfo": {
          "standard": "ERC20",
          "type": "Fungible",
          "contractAddress": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
          "symbol": "weth",
          "name": "WETH",
          "logo": "https://assets.coingecko.com/coins/images/2518/large/weth.png?1628852295",
          "decimals": 18,
          "dollarValue": "1834.6199951171875"
        },
        "type": "Transfer",
        "from": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "to": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
        "rawAmount": "0x58d15e17628000",
        "amount": "0.025",
        "dollarValue": "45.8654998779296875"
      },
      {
        "assetInfo": {
          "standard": "ERC20",
          "contractAddress": "0xd81781e686d0ad128b4c7e7b3c072b89f509ea2a"
        },
        "type": "Transfer",
        "from": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
        "to": "0x17b11ed010e715bf4336a88489fe4f0ef6a09dc7",
        "rawAmount": "0x4451132d60748"
      },
      {
        "assetInfo": {
          "standard": "NativeCurrency",
          "type": "Native",
          "symbol": "eth",
          "name": "Ethereum",
          "logo": "https://assets.coingecko.com/coins/images/279/large/ethereum.png?1595348880",
          "decimals": 18,
          "dollarValue": "1828.77001953125"
        },
        "type": "Transfer",
        "from": "0x17b11ed010e715bf4336a88489fe4f0ef6a09dc7",
        "to": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "rawAmount": "0x58d15e17628000",
        "amount": "0.025",
        "dollarValue": "45.71925048828125"
      },
      {
        "assetInfo": {
          "standard": "NativeCurrency",
          "type": "Native",
          "symbol": "eth",
          "name": "Ethereum",
          "logo": "https://assets.coingecko.com/coins/images/279/large/ethereum.png?1595348880",
          "decimals": 18,
          "dollarValue": "1828.77001953125"
        },
        "type": "Transfer",
        "from": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "to": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "rawAmount": "0x58d15e17628000",
        "amount": "0.025",
        "dollarValue": "45.71925048828125"
      }
    ],
    "balanceChanges": [
      {
        "address": "0x17b11ed010e715bf4336a88489fe4f0ef6a09dc7",
        "dollarValue": "-45.71925048828125",
        "transfers": [
          2,
          3
        ]
      },
      {
        "address": "0x7a250d5630b4cf539739df2c5dacb4c659f2488d",
        "dollarValue": "0",
        "transfers": [
          0,
          1,
          3,
          4
        ]
      },
      {
        "address": "0xa0c9bf9aa601ddfb1cdf3be3ef77e010e4184076",
        "dollarValue": "45.8654998779296875",
        "transfers": [
          1,
          2
        ]
      },
      {
        "address": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "dollarValue": "45.71925048828125",
        "transfers": [
          4
        ]
      }
    ]
  }
}
```
{% endtab %}
{% endtabs %}

**RESULT**: Trace transactions result `OBJECT`

* **status** `NUMBER:` either `1` (success) or `0` (failure)
* **gasUsed** `NUMBER`: The amount of gas used by this specific transaction alone
* **cumulativeGasUsed** `NUMBER`: the total amount of gas used when this transaction was executed in the block
* **blockNumber** `NUMBER`: the block number in which this transaction was simulated
* **type** `NUMBER`: transaction type, `0x00` for legacy transactions, `0x01` for access list types, `0x02` for dynamic fees
* **logsBloom** `STRING`: bloom filter for light clients to quickly retrieve related logs
* **logs**: an array of emitted events `ARRAY` of `OBJECT`
  * **name** `STRING`: event name
  * **anonymous** `BOOLEAN`: indicates if event is anonymous
  * **inputs**: array of decoded log arguments `ARRAY` of decoded logs `OBJECT`
    * **name** `STRING`: event argument name
    * **type** `STRING`: event argument type from Solidity type system
    * **value** (_optional_) `STRING` string representation value of the argument; interpret according to the `type` field
  * **raw** `OBJECT`: raw logs
    * **address** `STRING` hex encoded address: address of the contract emitting the log
    * **topics** `ARRAY` of `STRING` 32 hex encoded bytes
    * **data** `STRING` hex encoded string representing event data
* **trace**: Trace `ARRAY` of `OBJECT`
  * **type** `STRING` type: trace item type - either `CALL`| `CALLCODE`| `STATICCALL`| `DELEGATECALL`| `CREATE`| `CREATE2`| `SELFDESTRUCT`
  * **from** `STRING`: hex encoded address
  * **to** `STRING`: hex encoded address
  * **gas** `STRING`: hex encoded unsigned 64 byte integer representing event gas
  * **gasUsed** `STRING`: hex encoded unsigned 64 byte integer representing event gasUsed
  * **value** `STRING`: hex encoded unsigned 64 byte integer representing event value in wei
  * **error** `STRING`: low-level error from virtual machine
  * **errorReason** `STRING`: extracted error reason in case of revert
  * **input** `STRING`: hex encoded string representation of raw input bytes for the trace point
  * **method** `STRING`: invoked contract method
  * **decodedInput** : decoded input for the invoked method - `ARRAY` of decoded in argument `OBJECT`
    * **value** `STRING`: string representation value of the argument; interpret according to the `type` field.
    * **type** `STRING`: the Solidity type of this argument
    * **name** `STRING`: the name of this argument
  * **output** `STRING`: raw trace output
  * **decodedOutput** : decoded output of the invoked method - `ARRAY` of decoded out argument `OBJECT`
    * **value** `STRING`: string representation value of the argument; interpret according to the `type` field.
    * **type** `STRING`: the Solidity type of this argument
    * **name** `STRING`: the name of this argument
  * **subtraces** `NUMBER`: number of child traces
  * **traceAddress** : trace position `ARRAY` of `NUMBER`
* **`assetChanges`** `ARRAY`:&#x20;
  * **`type`** `STRING` type of asset change, can be transfer, mint, burn
  * **`from`** `STRING`: address of the sender (empty for mint transfers)
  * **`to`** `STRING`: address of the receiver (empty for burn transfers)
  * **`amount`** `STRING`: the amount of the token that was transferred
  * **`rawAmount`** `STRING`: raw amount transfer for the token
  * **`dollarValue`**`STRING`: dollar value of the transferred token
  * **`assetInfo`**`OBJECT`: asset information
    * **`standard`** `STRING`: supported token standards: ERC20, ERC721, NativeCurrency
    * **`type`** `STRING`: the token type: Native, Fungible, Non-Fungible
    * **`contractAddress`**`STRING` : address of the contract
    * **`symbol`** `STRING`: token symbol
    * **`name`** `STRING`: token name
    * **`logo`** `STRING`: URL for the token icon
    * **`decimals`** `NUMBER`: number of decimals in the token
    * **`dollarValue`**`STRING`: dollar value of a single token
* **`balanceChanges`** `ARRAY`: an array of balance changes - cumulated asset changes
  * **`address`** `STRING` address
  * **`dollarValue`** `STRING`: dollar value of cumulated asset changes
  * **`transfers`** `ARRAY`: array of asset changes indexes
