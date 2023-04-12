---
description: >-
  Learn how to execute a transaction bundle with Simulation Bundles using the
  Tenderly SDK.
---

# How to Perform Simulation Bundles with Tenderly SDK

In this tutorial, you'll learn how to use the Tenderly SDK to simulate bundled transactions. A bundled transaction is a collection of multiple transactions that are simulated as a unit.&#x20;

Bundled transactions are often used in DeFi protocols and other applications to simulate the process of performing complex operations that involve multiple contract interactions.

{% hint style="info" %}
Transactions from a bundle are simulated on the same blocks.
{% endhint %}

We'll simulate the usage of Uniswap for swapping a particular amount of DAI for WETH, and show the execution status of simulated transactions, and calculate the total gas used.

Here are the transactions needed to achieve this:

1. **Simulate minting of 2 DAI** so the swapper has some assets to swap. Alternatively, if you have DAI, you can skip this and just do transaction 2.
2. **Approve UniswapV3Router** to use DAI.
3. **Do the swap**. Call `UniswapV2Router.exactInputSingle` to perform the swap.

For the 1st transaction to run successfully, the sender needs to be a ward of DAI stablecoin. Since most of us aren't, we'll see how to use State Overrides to "become a ward" within the context of the Bundled Simulation.

### Prerequisites

* Node.js installed on your machine
* [Tenderly account with an API key](../../other/platform-access/how-to-generate-api-access-tokens.md)
* [Project set up in the Tenderly Dashboard](https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name)

### Step 1: Set up the project

Create a new npm project, install dependencies, and configure Typescript by pasting the following commands into your terminal:

```bash
mkdir tenderly-sdk-simulations
cd tenderly-sdk-simulations
npm init -y
yarn add @tenderly/sdk ethers
yarn add --dev typescript ts-node @types/node  dotenv
echo '{
  "compilerOptions": {
  "module": "commonjs",
  "esModuleInterop": true,
  "target": "es6",
  "moduleResolution": "node",
  "sourceMap": true,
  "outDir": "dist"
  "moduleResolution": "node16",
  },  
  "lib": ["es2015"]
}' > tsconfig.json

mkdir src
touch src/swap.ts
code .
```

### Step 2: Call the Simulation API

Copy the complete runnable example from below and paste it into the `swap.ts` file:

<details>

<summary>Complete runnable example (typescript)</summary>

```typescript
import { Interface, parseEther } from "ethers";
import { Tenderly } from "@tenderly/sdk";
import { Network } from "@tenderly/sdk";
import { TransactionParameters } from "@tenderly/sdk/lib/simulator";

const fakeWardAddressEOA = '0xe2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2e2';
const daiOwnerEOA = '0xe58b9ee93700a616b50509c8292977fa7a0f8ce1';
const daiAddressMainnet = '0x6b175474e89094c44da98b954eedeac495271d0f';
const uniswapV3SwapRouterAddressMainnet = '0xe592427a0aece92de3edee1f18e0157c05861564';
const wethAddressMainnet = '0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2';

(async () => {
  const tenderly = new Tenderly({
  accessKey: "access key",
  accountName: "your account name",
  projectName: "project-name-hyphenated",
  network: Network.MAINNET,
  });

  const simulatedBundle = await tenderly.simulator.simulateBundle({
  blockNumber: 0x103a957,
  transactions: [
    // TX1: Mint 2 DAI for daiOwnerEOA.
    // For minting to happen, we must do a state override so fakeWardAddress EOA is considered a ward for this simulation (see overrides)
    mint2DaiTx(),
    // TX2: daiOwnerEOA approves 1 DAI to uniswapV3SwapRouterAddressMainnet
    approveUniswapV3RouterTx(),
    // TX3: Perform a uniswap swap of 1/3 ETH
    swapSomeDaiForWethTx(),
  ],
  overrides: {
    [daiAddressMainnet]: {
    state: {
      // make DAI think that fakeWardAddress is a ward for minting
      [`wards[${fakeWardAddressEOA}]`]:
      '0x0000000000000000000000000000000000000000000000000000000000000001',
    },
    },
  },
  });
  const totalGasUsed = simulatedBundle
  .map(simulation => simulation.gasUsed)
  .reduce((total, gasUsed) => total + gasUsed);

  console.log('Total gas used:', totalGasUsed);

  simulatedBundle.forEach((simulation, idx) => {
  console.log(
    `Transaction ${idx} at block ${simulation.blockNumber}`,
    simulation.status ? 'success' : 'failed',
  );
  });

  console.log(JSON.stringify(simulatedBundle, null, 2));
})();

function mint2DaiTx(): TransactionParameters {
  return {
  from: fakeWardAddressEOA,
  to: daiAddressMainnet,
  gas: 0,
  gas_price: '0',
  value: 0,
  input: daiEthersInterface().encodeFunctionData('mint', [daiOwnerEOA, parseEther('2')]),
  };
}

function approveUniswapV3RouterTx(): TransactionParameters {
  return {
  from: daiOwnerEOA,
  to: daiAddressMainnet,
  gas: 0,
  gas_price: '0',
  value: 0,
  input: daiEthersInterface().encodeFunctionData('approve', [
    uniswapV3SwapRouterAddressMainnet,
    parseEther('1'),
  ]),
  };
}

function swapSomeDaiForWethTx(): TransactionParameters {
  return {
  from: daiOwnerEOA,
  to: uniswapV3SwapRouterAddressMainnet,
  gas: 0,
  gas_price: '0',
  value: 0,
  input: uniswapRouterV2EthersInterface().encodeFunctionData('exactInputSingle', [
    {
    tokenIn: daiAddressMainnet,
    tokenOut: wethAddressMainnet,
    fee: '10000',
    recipient: daiOwnerEOA,
    deadline: (1681109951 + 10 * 365 * 24 * 60 * 60 * 1000).toString(),
    amountIn: '33000000000000000',
    amountOutMinimum: '763124874493',
    sqrtPriceLimitX96: '0',
    },
  ]),
  };
}

function daiEthersInterface() {
  // prettier-ignore
  const daiAbi=[
  {constant:false,inputs:[{internalType:'address',name:'src',type:'address',},{internalType:'address',name:'dst',type:'address',},{internalType:'uint256',name:'wad',type:'uint256',},],name:'transferFrom',outputs:[{internalType:'bool',name:'',type:'bool',},],payable:false,stateMutability:'nonpayable',type:'function',},
  {constant:false,inputs:[{internalType:'address',name:'usr',type:'address',},{internalType:'uint256',name:'wad',type:'uint256',},],name:'approve',outputs:[{internalType:'bool',name:'',type:'bool',},],payable:false,stateMutability:'nonpayable',type:'function',},
  {constant:false,inputs:[{internalType:'address',name:'usr',type:'address',},{internalType:'uint256',name:'wad',type:'uint256',},],name:'mint',outputs:[],payable:false,stateMutability:'nonpayable',type:'function',}
  ];

  return new Interface(daiAbi);
}

function uniswapRouterV2EthersInterface() {
  //prettier-ignore
  const swapRouterAbi = [
  { inputs: [ { internalType: 'address', name: '_factory', type: 'address', }, { internalType: 'address', name: '_WETH9', type: 'address', }, ], stateMutability: 'nonpayable', type: 'constructor', },
  { inputs: [], name: 'WETH9', outputs: [ { internalType: 'address', name: '', type: 'address', }, ], stateMutability: 'view', type: 'function', },
  { inputs: [ { components: [ { internalType: 'bytes', name: 'path', type: 'bytes', }, { internalType: 'address', name: 'recipient', type: 'address', }, { internalType: 'uint256', name: 'deadline', type: 'uint256', }, { internalType: 'uint256', name: 'amountIn', type: 'uint256', }, { internalType: 'uint256', name: 'amountOutMinimum', type: 'uint256', }, ], internalType: 'struct ISwapRouter.ExactInputParams', name: 'params', type: 'tuple', }, ], name: 'exactInput', outputs: [ { internalType: 'uint256', name: 'amountOut', type: 'uint256', }, ], stateMutability: 'payable', type: 'function', },
  { inputs: [ { components: [ { internalType: 'address', name: 'tokenIn', type: 'address', }, { internalType: 'address', name: 'tokenOut', type: 'address', }, { internalType: 'uint24', name: 'fee', type: 'uint24', }, { internalType: 'address', name: 'recipient', type: 'address', }, { internalType: 'uint256', name: 'deadline', type: 'uint256', }, { internalType: 'uint256', name: 'amountIn', type: 'uint256', }, { internalType: 'uint256', name: 'amountOutMinimum', type: 'uint256', }, { internalType: 'uint160', name: 'sqrtPriceLimitX96', type: 'uint160', }, ], internalType: 'struct ISwapRouter.ExactInputSingleParams', name: 'params', type: 'tuple', }, ], name: 'exactInputSingle', outputs: [ { internalType: 'uint256', name: 'amountOut', type: 'uint256', }, ], stateMutability: 'payable', type: 'function', },
  { inputs: [ { components: [ { internalType: 'bytes', name: 'path', type: 'bytes', }, { internalType: 'address', name: 'recipient', type: 'address', }, { internalType: 'uint256', name: 'deadline', type: 'uint256', }, { internalType: 'uint256', name: 'amountOut', type: 'uint256', }, { internalType: 'uint256', name: 'amountInMaximum', type: 'uint256', }, ], internalType: 'struct ISwapRouter.ExactOutputParams', name: 'params', type: 'tuple', }, ], name: 'exactOutput', outputs: [ { internalType: 'uint256', name: 'amountIn', type: 'uint256', }, ], stateMutability: 'payable', type: 'function', },
  { inputs: [ { components: [ { internalType: 'address', name: 'tokenIn', type: 'address', }, { internalType: 'address', name: 'tokenOut', type: 'address', }, { internalType: 'uint24', name: 'fee', type: 'uint24', }, { internalType: 'address', name: 'recipient', type: 'address', }, { internalType: 'uint256', name: 'deadline', type: 'uint256', }, { internalType: 'uint256', name: 'amountOut', type: 'uint256', }, { internalType: 'uint256', name: 'amountInMaximum', type: 'uint256', }, { internalType: 'uint160', name: 'sqrtPriceLimitX96', type: 'uint160', }, ], internalType: 'struct ISwapRouter.ExactOutputSingleParams', name: 'params', type: 'tuple', }, ], name: 'exactOutputSingle', outputs: [ { internalType: 'uint256', name: 'amountIn', type: 'uint256', }, ], stateMutability: 'payable', type: 'function', },
  { inputs: [], name: 'factory', outputs: [ { internalType: 'address', name: '', type: 'address', }, ], stateMutability: 'view', type: 'function', },
  { inputs: [ { internalType: 'bytes[]', name: 'data', type: 'bytes[]', }, ], name: 'multicall', outputs: [ { internalType: 'bytes[]', name: 'results', type: 'bytes[]', }, ], stateMutability: 'payable', type: 'function', },
  { inputs: [], name: 'refundETH', outputs: [], stateMutability: 'payable', type: 'function', },
  { inputs: [ { internalType: 'address', name: 'token', type: 'address', }, { internalType: 'uint256', name: 'value', type: 'uint256', }, { internalType: 'uint256', name: 'deadline', type: 'uint256', }, { internalType: 'uint8', name: 'v', type: 'uint8', }, { internalType: 'bytes32', name: 'r', type: 'bytes32', }, { internalType: 'bytes32', name: 's', type: 'bytes32', }, ], name: 'selfPermit', outputs: [], stateMutability: 'payable', type: 'function', },
  { inputs: [ { internalType: 'address', name: 'token', type: 'address', }, { internalType: 'uint256', name: 'nonce', type: 'uint256', }, { internalType: 'uint256', name: 'expiry', type: 'uint256', }, { internalType: 'uint8', name: 'v', type: 'uint8', }, { internalType: 'bytes32', name: 'r', type: 'bytes32', }, { internalType: 'bytes32', name: 's', type: 'bytes32', }, ], name: 'selfPermitAllowed', outputs: [], stateMutability: 'payable', type: 'function', },
  { inputs: [ { internalType: 'address', name: 'token', type: 'address', }, { internalType: 'uint256', name: 'nonce', type: 'uint256', }, { internalType: 'uint256', name: 'expiry', type: 'uint256', }, { internalType: 'uint8', name: 'v', type: 'uint8', }, { internalType: 'bytes32', name: 'r', type: 'bytes32', }, { internalType: 'bytes32', name: 's', type: 'bytes32', }, ], name: 'selfPermitAllowedIfNecessary', outputs: [], stateMutability: 'payable', type: 'function', },
  { inputs: [ { internalType: 'address', name: 'token', type: 'address', }, { internalType: 'uint256', name: 'value', type: 'uint256', }, { internalType: 'uint256', name: 'deadline', type: 'uint256', }, { internalType: 'uint8', name: 'v', type: 'uint8', }, { internalType: 'bytes32', name: 'r', type: 'bytes32', }, { internalType: 'bytes32', name: 's', type: 'bytes32', }, ], name: 'selfPermitIfNecessary', outputs: [], stateMutability: 'payable', type: 'function', },
  { inputs: [ { internalType: 'address', name: 'token', type: 'address', }, { internalType: 'uint256', name: 'amountMinimum', type: 'uint256', }, { internalType: 'address', name: 'recipient', type: 'address', }, ], name: 'sweepToken', outputs: [], stateMutability: 'payable', type: 'function', },
  { inputs: [ { internalType: 'address', name: 'token', type: 'address', }, { internalType: 'uint256', name: 'amountMinimum', type: 'uint256', }, { internalType: 'address', name: 'recipient', type: 'address', }, { internalType: 'uint256', name: 'feeBips', type: 'uint256', }, { internalType: 'address', name: 'feeRecipient', type: 'address', }, ], name: 'sweepTokenWithFee', outputs: [], stateMutability: 'payable', type: 'function', },
  { inputs: [ { internalType: 'int256', name: 'amount0Delta', type: 'int256', }, { internalType: 'int256', name: 'amount1Delta', type: 'int256', }, { internalType: 'bytes', name: '_data', type: 'bytes', }, ], name: 'uniswapV3SwapCallback', outputs: [], stateMutability: 'nonpayable', type: 'function', }, { inputs: [ { internalType: 'uint256', name: 'amountMinimum', type: 'uint256', }, { internalType: 'address', name: 'recipient', type: 'address', }, ], name: 'unwrapWETH9', outputs: [], stateMutability: 'payable', type: 'function', }, { inputs: [ { internalType: 'uint256', name: 'amountMinimum', type: 'uint256', }, { internalType: 'address', name: 'recipient', type: 'address', }, { internalType: 'uint256', name: 'feeBips', type: 'uint256', }, { internalType: 'address', name: 'feeRecipient', type: 'address', }, ], name: 'unwrapWETH9WithFee', outputs: [], stateMutability: 'payable', type: 'function', }, { stateMutability: 'payable', type: 'receive', }
  ];

  return new Interface(swapRouterAbi);
}
```



</details>

Further down in the tutorial, you'll find detailed explanations of what the code is doing.&#x20;

### Step 3: Run the script

```bash
npx ts-node src/swap.ts
```

### Understanding the code

First, we're creating a new instance of the Tenderly SDK:

```typescript
const tenderly = new Tenderly({
  accessKey: "access key",
  accountName: "your account name",
  projectName: "project-name-hyphenated",
  network: Network.MAINNET,
});
```

To call the Simulations API and perform a bundled simulation, we're using `Tenderly.simulator.simulateBundle()` and passing an object with the following fields:

* `blockNumber` - the block number on which you wish to execute the simulation.
* `transactions` - an array holding three transactions: minting of 2 DAI, approving the Uniswap Router, and swapping DAI for WETH.
* `overrides` - an object making `fakeWardAddress` a ward of DAI within the simulation.

```typescript
const simulatedBundle = await tenderly.simulator.simulateBundle({
  blockNumber: 0x103a957,
  transactions: [
    // TX1: Mint 2 DAI for daiOwnerEOA.
    // For minting to happen, we must do a state override so fakeWardAddressEOA is considered a ward for this simulation (see overrides below)
    mint2DaiTx(),
    // TX2: daiOwnerEOA approves 1 DAI to uniswapV3SwapRouterAddressMainnet
    approveUniswapV3RouterTx(),
    // TX3: Perform a uniswap swap of 1/3 ETH
    swapSomeDaiForWethTx(),
  ],
  overrides: {
    [daiAddressMainnet]: {
      state: {
        // make DAI think that fakeWardAddress is a ward for minting
        [`wards[${fakeWardAddressEOA}]`]:
        '0x0000000000000000000000000000000000000000000000000000000000000001',
      },
    },
  },
  });
```

Below you'll find the functions which are responsible for producing the three transactions:

{% tabs %}
{% tab title="mint2DaiTx " %}
```typescript
function mint2DaiTx(): TransactionParameters {
  return {
    from: fakeWardAddressEOA,
    to: daiAddressMainnet,
    gas: 0,
    gas_price: '0',
    value: 0,
    input: daiEthersInterface()
           .encodeFunctionData('mint', [daiOwnerEOA, parseEther('2')]),
  };
}

function daiEthersInterface() {
  const daiAbi = [
    {constant:false,inputs:[{internalType:'address',name:'src',type:'address',},{internalType:'address',name:'dst',type:'address',},{internalType:'uint256',name:'wad',type:'uint256',},],name:'transferFrom',outputs:[{internalType:'bool',name:'',type:'bool',},],payable:false,stateMutability:'nonpayable',type:'function',},
    {constant:false,inputs:[{internalType:'address',name:'usr',type:'address',},{internalType:'uint256',name:'wad',type:'uint256',},],name:'approve',outputs:[{internalType:'bool',name:'',type:'bool',},],payable:false,stateMutability:'nonpayable',type:'function',},
    {constant:false,inputs:[{internalType:'address',name:'usr',type:'address',},{internalType:'uint256',name:'wad',type:'uint256',},],name:'mint',outputs:[],payable:false,stateMutability:'nonpayable',type:'function',}
  ];

  return new Interface(daiAbi);
}
```
{% endtab %}

{% tab title="approveUniswapV3RouterTx" %}
```typescript

function approveUniswapV2RouterTx(): TransactionParameters {
  return {
    from: daiOwnerEOA,
    to: daiAddressMainnet,
    gas: 0,
    gas_price: '0',
    value: 0,
    input: daiEthersInterface()
           .encodeFunctionData('approve', [
             uniswapV3SwapRouterAddressMainnet,
             parseEther('1'),
           ]),
  };
}

function daiEthersInterface() {
  const daiAbi = [
    {constant:false,inputs:[{internalType:'address',name:'src',type:'address',},{internalType:'address',name:'dst',type:'address',},{internalType:'uint256',name:'wad',type:'uint256',},],name:'transferFrom',outputs:[{internalType:'bool',name:'',type:'bool',},],payable:false,stateMutability:'nonpayable',type:'function',},
    {constant:false,inputs:[{internalType:'address',name:'usr',type:'address',},{internalType:'uint256',name:'wad',type:'uint256',},],name:'approve',outputs:[{internalType:'bool',name:'',type:'bool',},],payable:false,stateMutability:'nonpayable',type:'function',},
    {constant:false,inputs:[{internalType:'address',name:'usr',type:'address',},{internalType:'uint256',name:'wad',type:'uint256',},],name:'mint',outputs:[],payable:false,stateMutability:'nonpayable',type:'function',}
  ];

  return new Interface(daiAbi);
}
```
{% endtab %}

{% tab title="swapSomeDaiForWethTx" %}
```typescript
function swapSomeDaiForWethTx(): TransactionParameters {
  return {
    from: daiOwnerEOA,
    to: uniswapV3SwapRouterAddressMainnet,
    gas: 0,
    gas_price: '0',
    value: 0,
    input: uniswapRouterV2EthersInterface()
           .encodeFunctionData('exactInputSingle', [{
              tokenIn: daiAddressMainnet,
              tokenOut: wethAddressMainnet,
              fee: '10000',
              recipient: daiOwnerEOA,
              deadline: (317041109951).toString(), // until Apr 2033
              amountIn: '33000000000000000',
              amountOutMinimum: '763124874493',
              sqrtPriceLimitX96: '0',
            }]),
  };
  
function uniswapRouterV2EthersInterface() {
  const swapRouterAbi = [
    { inputs: [ { internalType: 'address', name: '_factory', type: 'address', }, { internalType: 'address', name: '_WETH9', type: 'address', }, ], stateMutability: 'nonpayable', type: 'constructor', },
    ...
    { inputs: [ { internalType: 'int256', name: 'amount0Delta', type: 'int256', }, { internalType: 'int256', name: 'amount1Delta', type: 'int256', }, { internalType: 'bytes', name: '_data', type: 'bytes', }, ], name: 'uniswapV3SwapCallback', outputs: [], stateMutability: 'nonpayable', type: 'function', }, { inputs: [ { internalType: 'uint256', name: 'amountMinimum', type: 'uint256', }, { internalType: 'address', name: 'recipient', type: 'address', }, ], name: 'unwrapWETH9', outputs: [], stateMutability: 'payable', type: 'function', }, { inputs: [ { internalType: 'uint256', name: 'amountMinimum', type: 'uint256', }, { internalType: 'address', name: 'recipient', type: 'address', }, { internalType: 'uint256', name: 'feeBips', type: 'uint256', }, { internalType: 'address', name: 'feeRecipient', type: 'address', }, ], name: 'unwrapWETH9WithFee', outputs: [], stateMutability: 'payable', type: 'function', }, { stateMutability: 'payable', type: 'receive', }
  ];

  return new Interface(swapRouterAbi);
}
```
{% endtab %}
{% endtabs %}

### Understanding State Overrides

We're calling the DAI stablecoin `mint` function. During the simulation, the DAI contract has to believe you (the sender) are one of the wards. Otherwise, it will reject to mint.&#x20;

We need the following condition to hold for DAI contract's state for a successful minting initiated by `fakeWardAddressEOA`:

```typescript
daiAddressMainnet.state.wards[fakeWardAddressEOA] == 0x0000...0001
```

To enable this, we're passing `overrides` to the SDK, where we're overriding the DAI `wards` storage variable, so `fakeDaiWardAddress` becomes a ward during the simulation.

<pre class="language-typescript"><code class="lang-typescript"><strong>overrides: {
</strong>  [daiAddressMainnet]: {
    state: {
        // make DAI think that fakeWardAddress is a ward for minting
        [`wards[${fakeWardAddressEOA}]`]:
        '0x0000000000000000000000000000000000000000000000000000000000000001',
    },
  },
<strong>},
</strong></code></pre>

{% hint style="info" %}
Note that the overrides apply to the **entire bundle** and are visible to all simulations within the bundle.
{% endhint %}

Now, you have a better understanding of how to use the Tenderly SDK to perform complex simulation scenarios and display essential results.
