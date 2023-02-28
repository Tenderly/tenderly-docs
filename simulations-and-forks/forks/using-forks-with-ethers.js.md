---
description: Learn how to use the Fork JSON-RPC as Ethers.js JSONRpcProvider.
---

# Using Forks With Ethers.js

The following code sample will guide you through:

* Creating a Fork using the Fork API with custom chain config.
* Connecting Ethers.js to the Fork.
* Completing a Fork state override.
* Sending several transactions.

In this example, we'll mint, approve, and transferFrom some DAI. We'll use the Mainnet Dai contract:

1. **TX1 – mint:** We'll use an arbitrary address ($minter) to mint 2 DAI for $owner.
2. **TX2 – approve:** The address $owner will approve $spender to spend 0.5 DAI.
3. **TX3 – transferFrom:** The address we just approved ($spender) will transfer 0.25 DAI to $receiver.

We have three participants in this scenario: $minter, $spender, and $receiver. Instead of dealing with real addresses, we'll use accounts available on the Fork upon creation (lines 29..32).

{% code overflow="wrap" lineNumbers="true" %}
```typescript
import axios from 'axios';
import * as dotenv from 'dotenv';
import { ethers } from 'ethers';

dotenv.config();

// assuming environment variables TENDERLY_USER, TENDERLY_PROJECT and TENDERLY_ACCESS_KEY are set
// https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name
// https://docs.tenderly.co/other/platform-access/how-to-generate-api-access-tokens
const { TENDERLY_USER, TENDERLY_PROJECT, TENDERLY_ACCESS_KEY } = process.env;

const daiOnFork = async () => {
  console.time('Fork Creation');
  const fork = await mainnetFork();
  console.timeEnd('Fork Creation');

  const forkId = fork.data.simulation_fork.id;
  const rpcUrl = `https://rpc.tenderly.co/fork/${forkId}`;
  // const rpcUrl =
  //   'https://rpc.tenderly.co/fork/44abcc89-ed65-43bf-baa7-d3bc1e34feb7';
  console.log('Fork URL\n\t' + rpcUrl);

  const forkProvider = new ethers.providers.JsonRpcProvider(rpcUrl);

  const [minterAddress, ownerAddress, spenderAddress, receiverAddress] =
    await forkProvider.listAccounts();

  const [minterSigner, ownerSigner, spenderSigner] = [
    forkProvider.getSigner(minterAddress),
    forkProvider.getSigner(ownerAddress),
    forkProvider.getSigner(spenderAddress),
    forkProvider.getSigner(receiverAddress),
  ];

  /*
  // alternatively, you could as well use an existing account you do have private key access to.

  const minterAddress = '0xdc6bdc37b2714ee601734cf55a05625c9e512461';
  const minterSigner = new ethers.Wallet(
    '0x94...5c'
  ).connect(forkProvider);

    await forkProvider.send('tenderly_setBalance', [
      [minterAddress],
      ethers.utils.hexValue(ethers.utils.parseUnits('10', 'ether').toHexString()),
    ]);

  */

  // override: make 0xdc6bdc37b2714ee601734cf55a05625c9e512461 a ward of DAI
  await forkProvider.send('tenderly_setStorageAt', [
    // the DAI contract address
    '0x6b175474e89094c44da98b954eedeac495271d0f',
    // storage location wards['0xdc6bdc37b2714ee601734cf55a05625c9e512461']
    ethers.utils.keccak256(
      ethers.utils.concat([
        ethers.utils.hexZeroPad(minterAddress, 32), // the ward address (address 0x000..0) - mapping key
        ethers.utils.hexZeroPad('0x0', 32), // the wards slot is 0th  in the DAI contract - the mapping variable
      ])
    ),
    // flag 1 (at 32 bytes length)
    '0x0000000000000000000000000000000000000000000000000000000000000001',
  ]);

  // TX1: mint
  await minterSigner.sendTransaction({
    from: minterAddress,
    to: '0x6b175474e89094c44da98b954eedeac495271d0f',
    data: DaiAbi.encodeFunctionData('mint', [
      ethers.utils.hexZeroPad(ownerAddress.toLowerCase(), 20),
      ethers.utils.parseEther('1.0'),
    ]),
    gasLimit: 800000,
  });

  // TX2: approve
  await ownerSigner.sendTransaction({
    to: '0x6b175474e89094c44da98b954eedeac495271d0f',
    data: DaiAbi.encodeFunctionData('approve', [
      ethers.utils.hexZeroPad(spenderAddress.toLowerCase(), 20),
      ethers.utils.parseEther('1.0'),
    ]),
    gasLimit: 800000,
  });

  // TX3: transferFrom
  await spenderSigner.sendTransaction({
    to: '0x6b175474e89094c44da98b954eedeac495271d0f',
    data: DaiAbi.encodeFunctionData('transferFrom', [
      ethers.utils.hexZeroPad(ownerAddress.toLowerCase(), 20),
      ethers.utils.hexZeroPad(receiverAddress.toLowerCase(), 20),
      ethers.utils.parseEther('1.0'),
    ]),
    gasLimit: 800000,
  });

  // deleteFork(forkId);
};

const DaiAbi = new ethers.utils.Interface([
  {
    constant: false,
    inputs: [
      { internalType: 'address', name: 'usr', type: 'address' },
      { internalType: 'uint256', name: 'wad', type: 'uint256' },
    ],
    name: 'mint',
    outputs: [],
    payable: false,
    stateMutability: 'nonpayable',
    type: 'function',
  },
  {
    constant: false,
    inputs: [
      { internalType: 'address', name: 'usr', type: 'address' },
      { internalType: 'uint256', name: 'wad', type: 'uint256' },
    ],
    name: 'approve',
    outputs: [{ internalType: 'bool', name: '', type: 'bool' }],
    payable: false,
    stateMutability: 'nonpayable',
    type: 'function',
  },
  {
    constant: false,
    inputs: [
      { internalType: 'address', name: 'src', type: 'address' },
      { internalType: 'address', name: 'dst', type: 'address' },
      { internalType: 'uint256', name: 'wad', type: 'uint256' },
    ],
    name: 'transferFrom',
    outputs: [{ internalType: 'bool', name: '', type: 'bool' }],
    payable: false,
    stateMutability: 'nonpayable',
    type: 'function',
  },
]);

daiOnFork();

function deleteFork(forkId: any) {
  axios.delete(
    `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/fork/${forkId}`,
    {
      headers: {
        'X-Access-Key': TENDERLY_ACCESS_KEY as string,
      },
    }
  );
}

async function mainnetFork() {
  return await axios.post(
    `https://api.tenderly.co/api/v1/account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}/fork`,
    {
      network_id: '1',
      chain_config: {
        chain_id: 11,
        shanghai_time: 1677557088,
      },
    },
    {
      headers: {
        'X-Access-Key': TENDERLY_ACCESS_KEY as string,
      },
    }
  );
}

```
{% endcode %}
