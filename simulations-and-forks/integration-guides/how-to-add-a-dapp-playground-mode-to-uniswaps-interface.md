---
description: >-
  Learn how to build a dapp playground mode for Uniswap's UI using Tenderly
  Forks.
---

# How to Add a Dapp Playground Mode to Uniswap's Interface

In this guide, we'll walk you through the process of creating a dapp playground mode and adding it to Uniswap's open-source UI, using [Tenderly Forks](https://docs.tenderly.co/simulations-and-forks/forks) as the core infrastructure. The publicly shared Fork used in this example is [accessible here](https://dashboard.tenderly.co/shared/fork/67f626f2-e31e-4719-8bf2-8d2160d2218f/transactions), where you can view transactions and inspect them using Debugger without a Tenderly account.

To preview the end result, check out the video below, which shows you how playground mode in Uniswap's UI works.&#x20;

You can find the [complete demo repository on GitHub](https://github.com/Tenderly/uniswap-playground-mode).

{% embed url="https://youtu.be/rkpBUPMitUc" %}

{% hint style="info" %}
This tutorial is for demonstration purposes only, specifically to illustrate how to add a playground capability to a dapp. It is not intended nor recommended for any other usage.
{% endhint %}

## Why do dapps need playground mode?

Adding playground mode to dapps brings about two key benefits: building trust with end users and enabling easier onboarding to your dapp. Playground mode provides a safe environment where users can familiarize themselves with the features and core functionality of your dapp without risking real funds.

Transactions in playground mode are simulated within a virtual environment, protecting users from costly mistakes. In fact, playground mode can help users identify potential errors before they make it to the blockchain.

Beyond building trust, playground mode can also be helpful with easier onboarding of users to your dapp. It can make your dapp more approachable, drawing in new users. Furthermore, it can help users discover new ways to use your dapp, helping them tailor their interactions to suit their specific needs.

## How to make a dapp playground mode?

Dapps operating in playground mode never communicate with the live network. Instead, they interact with a cloned and isolated version of the blockchain's most recent state, referred to as a Fork.&#x20;

This is illustrated in the diagram below, with the playground mode depicted by yellow lines and the live network by grey lines.

<figure><img src="../../.gitbook/assets/28_Playground Mode-Inblog Illustration-02.png" alt=""><figcaption></figcaption></figure>

Upon entering playground mode, users are given a virtualized environment. Here, they can perform and test transactions without any risk as they are working with a replica of their chosen network.

To implement playground mode, dapps can use Tenderly Forks as the underlying infrastructure. All actions carried out in playground mode occur on a real-time replica of the latest state of the network, providing a realistic user experience.&#x20;

Moreover, Tenderly provides a transaction explorer where users can review simulated transactions. These transactions can be [kept private or shared publicly](https://blog.tenderly.co/changelog/public-sharing-of-transactions-devnets-forks-and-simulations/). This way, dapp users get all the tools to interact with the simulated dapp in familiar ways, resembling the live project.

## Uniswap playground mode - Project overview

As mentioned above, we’ll be adding a playground mode option to the Uniswap UI.

If you want to replicate the steps outlined in this tutorial, you should be familiar with Reach and how [Tenderly’s API](https://docs-api.tenderly.co/) works.

Here’s what we’ll need to do:

* Integrate Tenderly Fork API calls
* Create React hooks that put the dapp in playground mode. The hooks need to be able to:
  * Spin up a new Tenderly Fork through the API when playground mode activated
  * Add the Fork URL to the wallet (we’ll be using MetaMask)
  * Use Tenderly’s custom [Fork JSON RPC call `tenderly_setBalance`](https://docs.tenderly.co/devnets/advanced/custom-rpc-methods#tenderly\_setbalance) to top up the user’s account
* Create the Playground Controls Component
* Add the Playground Component to the UI
* Let the user know when playground mode is enabled



Let’s start building! 👷‍♂️

### Step 1: Clone the Uniswap UI from GitHub

Clone the GitHub repo that contains Uniswap’s open-source UI and install dependencies by running the following commands:

```bash
git clone https://github.com/Uniswap/interface.git
cd interface
yarn
```

You can find the complete [repository on GitHub](https://github.com/Tenderly/uniswap-playground-mode), including the changes we omitted from this guide.

### Step 2: Build out the logic for interacting with the Tenderly API

Write the logic to interact with the Tenderly API to handle the process of spinning up and deleting Tenderly Forks.

First, create a file called `tenderly-fork-api.ts`, where we’ll store the logic.

```bash
touch tenderly-fork-api.ts
```

Copy the code below and paste it into the file we created.

The provided JavaScript code exports two primary elements: `aTenderlyFork` function and `TenderlyForkProvider` type. It also utilizes the `@ethersproject/providers` and `axios` libraries and uses environment variables to set certain parameters.

Here is a breakdown of the main components:

1. **`aTenderlyFork` function**: This async function takes a `TenderlyForkRequest` object as an argument and returns a `TenderlyForkProvider` object. This function:
   * Sends a `POST` request to Tenderly's API to create a new fork.
   * Retrieves the ID of the fork created from the response data.
   * Generates a `rpcUrl` for the fork and uses it to create a `JsonRpcProvider`.
   * Creates `privateUrl` and `publicUrl` (URL that can be shared publicly) for the fork dashboard.
   * Returns an object of type `TenderlyForkProvider` with all the relevant details of the fork, including a `removeFork` method.
2. **`removeFork` function**: This async function takes  `forkId` as an argument and sends a `DELETE` request to Tenderly's API to remove a fork with the given ID.
3. **`tenderlyBaseApi` instance**: This is an instance of Axios with pre-configured `baseURL` and headers for communicating with Tenderly's API.

```tsx
import { JsonRpcProvider } from '@ethersproject/providers'
import axios, { AxiosResponse } from 'axios'

const { REACT_APP_TENDERLY_PROJECT_SLUG, REACT_APP_TENDERLY_ACCESS_KEY, REACT_APP_TENDERLY_USERNAME } = process.env

export async function aTenderlyFork(fork: TenderlyForkRequest): Promise<TenderlyForkProvider> {
  const forkResponse = await tenderlyBaseApi.post(
    `account/${REACT_APP_TENDERLY_USERNAME}/project/${REACT_APP_TENDERLY_PROJECT_SLUG}/fork/`,
    fork
  )

  const forkId = forkResponse.data.root_transaction.fork_id

  const rpcUrl = `https://rpc.tenderly.co/fork/${forkId}`
  const forkProvider = new JsonRpcProvider(rpcUrl)

  const blockNumberStr = (forkResponse.data.root_transaction.receipt.blockNumber as string).replace('0x', '')
  const blockNumber = Number.parseInt(blockNumberStr, 16)
  const privateUrl = `https://dashboard.tenderly.co/account/${REACT_APP_TENDERLY_USERNAME}/project/${REACT_APP_TENDERLY_PROJECT_SLUG}/fork/${forkId}`
  const publicUrl = `https://dashboard.tenderly.co/shared/fork/${forkId}/transactions`

  console.info(
    `\nForked ${fork.network_id} 
  at block ${blockNumber} 
  with chain ID ${fork.chain_config?.chain_id}
  fork ID: ${forkId} 
`
  )
  console.info('Fork:', privateUrl)

  return {
    rpcUrl,
    provider: forkProvider,
    blockNumber,
    forkUUID: forkId,
    removeFork: () => removeFork(forkId),
    networkId: fork.network_id as any,
    publicUrl,
    privateUrl,
    chainId: forkResponse.data.simulation_fork.chain_config.chain_id,
    baseChainId: fork.network_id,
  }
}

async function removeFork(forkId: string) {
  console.log('Removing test fork', forkId)
  return await tenderlyBaseApi.delete(
    `account/${REACT_APP_TENDERLY_USERNAME}/project/${REACT_APP_TENDERLY_PROJECT_SLUG}/fork/${forkId}`
  )
}

const tenderlyBaseApi = axios.create({
  baseURL: `https://api.tenderly.co/api/v1/`,
  headers: {
    'X-Access-Key': REACT_APP_TENDERLY_ACCESS_KEY || '',
    'Content-Type': 'application/json',
  },
})

type TenderlyForkRequest = {
  shared?: boolean
  block_number?: number
  network_id: string
  transaction_index?: number
  initial_balance?: number
  alias?: string
  description?: string
  chain_config?: {
    chain_id?: number
    homestead_block?: number
    dao_fork_support?: boolean
    eip_150_block?: number
    eip_150_hash?: string
    eip_155_block?: number
    eip_158_block?: number
    byzantium_block?: number
    constantinople_block?: number
    petersburg_block?: number
    istanbul_block?: number
    berlin_block?: number
  }
}

export type TenderlyForkProvider = {
  rpcUrl: string
  provider: JsonRpcProvider
  forkUUID: string
  blockNumber: number
  chainId: number
  networkId: number
  publicUrl: string
  privateUrl: string
  baseChainId: string
  /**
   * map from address to given address' balance
   */
  removeFork: () => Promise<AxiosResponse<any>>
}
```

### **Step 3: Add React hooks to enable playground mode**

Create a file with the name `useTenderlyFork.ts` and paste the code below into it.

This block of code contains React hooks that will be used to manage Tenderly Forks (i.e., replicas of the latest state of the chosen blockchain).

The most important hooks and functions to take note of include:

1. **`useActiveTenderlyFork` function**: Returns an object containing information about the current fork, including whether a fork is active and the fork's provider (an instance of **TenderlyForkProvider** or undefined).
2. **`useTenderlyPlayground` function**: Returns an object containing methods and data to manage a blockchain fork for testing or playground purposes. It includes:
   * **playgroundProvider**: The current fork provider.
   * **isPlayground**: A boolean indicating whether a fork is currently active.
   * **aNewPlayground**: A method for creating a new fork.
   * **discardPlayground**: A method for removing the current fork.
3. **`useNewFork` function**: This function is used to create a new fork of the blockchain. If there is an existing fork, it attempts to remove it first. Then, it creates a new fork using the specified or current chain ID and sets this new fork as the current provider. The new fork is also added to MetaMask, and the connected signer is topped up with Ether for testing purposes.
4. **`topUpConnectedSigner` function**: Used to provide a balance of Ether to the connected signer on the newly forked blockchain.
5. **`addForkToMetamask` function**: Adds the newly created fork to Metamask, an Ethereum wallet.
6. **`useRemoveFork` function**: Removes the current fork of the blockchain.

{% hint style="info" %}
When simulating a network using Tenderly Forks, we’re basing it on an existing network. To prevent a [transaction replay attack](https://quantstamp.com/blog/preventing-replay-attacks-post-ethereum-merge), we must specify the `chainId` that is different from the original network’s `chainId`. This is why we’re prefixing `chainId` before calling the Tenderly Fork API. We’re using the`TENDERLY_CHAIN_FORK_PREFIX`, which has an arbitrary value of `7340317`.
{% endhint %}

```tsx
import { useWeb3React } from '@web3-react/core'
import { aTenderlyFork, TenderlyForkProvider } from 'components/Web3Status/tenderly-fork-api'
import { removeTenderlyChainIdPrefix, TENDERLY_CHAIN_FORK_PREFIX } from 'constants/chains'
import { nativeOnChain } from 'constants/tokens'
// eslint-disable-next-line @typescript-eslint/no-restricted-imports
import { ethers } from 'ethers'
import { atom } from 'jotai'
import { useAtomValue, useUpdateAtom } from 'jotai/utils'
import { useCallback } from 'react'

const provider = atom<TenderlyForkProvider | undefined>(undefined)
const providerState = atom<'CREATING' | 'RUNNING'>('RUNNING')

export function useActiveTenderlyFork() {
  return { tenderlyFork: useAtomValue(provider) != null, forkProvider: useAtomValue(provider) || undefined }
}

export function useTenderlyPlayground(): {
  playgroundProvider?: TenderlyForkProvider
  isPlayground: boolean
  aNewPlayground: (chainId?: number) => Promise<void>
  discardPlayground: () => Promise<void>
} {
  const prov = useAtomValue(provider)
  return {
    playgroundProvider: prov,
    isPlayground: !!prov,
    aNewPlayground: useNewFork(),
    discardPlayground: useRemoveFork(),
  }
}

function useNewFork() {
  const currentProvider = useAtomValue(provider)
  const updateProvider = useUpdateAtom(provider)
  const updateProviderState = useUpdateAtom(providerState)
  const currentChainId = useWeb3React().chainId

  return useCallback(
    async (chainId: number | undefined = -1) => {
      if (currentProvider) {
        console.log('removing provider', currentProvider.rpcUrl)
        try {
          await currentProvider.removeFork()
        } catch (error) {
          console.warn('Errored out when deleting the old fork', error)
        }
      } else {
        console.log('no fork provider')
      }

      updateProviderState('CREATING')

      if (chainId == -1 && currentChainId) {
        chainId = currentChainId
      }
      chainId = removeTenderlyChainIdPrefix(chainId)
      const _forkProvider = await aTenderlyFork({
        network_id: '' + chainId,
        chain_config: { chain_id: Number.parseInt(`${TENDERLY_CHAIN_FORK_PREFIX}${chainId}`) },
        shared: true,
      })
      updateProvider(_forkProvider)
      await addForkToMetamask(_forkProvider)
      await topUpConnectedSigner(_forkProvider)
    },
    [currentProvider, updateProvider, updateProviderState, currentChainId]
  )
}

async function topUpConnectedSigner(forkProvider: TenderlyForkProvider) {
  if (window.ethereum) {
    const provider = new ethers.providers.Web3Provider(window.ethereum)
    const signer = provider.getSigner()

    console.log('Address', await signer.getAddress())
    console.log('top up: Fork provider', forkProvider.rpcUrl)

    await forkProvider.provider.send('tenderly_setBalance', [
      [await signer.getAddress()],
      ethers.utils.hexValue(ethers.utils.parseUnits('100', 'ether').toHexString()),
    ])

    const balanceRead = await forkProvider.provider.send('eth_getBalance', [await signer.getAddress(), 'latest'])

    console.log(`Balance of ${signer.getAddress()} is ${balanceRead}`)
  }
}

async function addForkToMetamask(forkProvider: TenderlyForkProvider) {
  const forkUrl = forkProvider.rpcUrl
  if (!forkUrl) {
    console.log('No Fork')
    return
  }

  if (typeof window.ethereum !== 'undefined') {
    const noc = nativeOnChain(forkProvider.chainId)
    //@ts-ignore
    await window.ethereum.request({
      method: 'wallet_addEthereumChain',
      params: [
        {
          chainId: `0x${forkProvider.chainId.toString(16)}`,
          rpcUrls: [forkUrl],
          chainName: `Forked ${forkProvider.chainId}`,
          nativeCurrency: {
            name: noc.name,
            symbol: noc.symbol,
            decimals: noc.decimals,
          },
          blockExplorerUrls: ['https://polygonscan.com/'],
        },
      ],
    })
  } else {
    console.log('Metamask is not installed')
  }
}

function useRemoveFork() {
  const currentProvider = useAtomValue(provider)
  const setProvider = useUpdateAtom(provider)
  return useCallback(async () => {
    await currentProvider?.removeFork()
    setProvider(undefined)
  }, [currentProvider, setProvider])
}
```

### Step 3: Create the Playground Controls Component

Next, we want to create controls that will put the dapp into playground mode. Create a file `PlaygroundControls.tsx` and paste the code below.

This JavaScript code defines a React component called `PlaygroundControls`, which provides a user interface for managing Tenderly Forks.

Here are the main components and their functionality:

1. **Hooks** are used to extract the required data and functionality:
   * `useTenderlyPlayground`: to control and manage the blockchain fork. This includes creating a new fork, checking if a fork is active, and discarding a fork.
2. **Button interactions** are defined within `createPlayground` and `connectChain` callbacks. `createPlayground` creates a new fork on click. `connectChain` switches to the original blockchain and discards the current fork.

```tsx
// PlaygroundControls.tsx
import { useWeb3React } from '@web3-react/core'
import useSelectChain from 'hooks/useSelectChain'
import useSyncChainQuery from 'hooks/useSyncChainQuery'
import { useTenderlyPlayground } from 'hooks/useTenderlyFork'
import useBlockNumber from 'lib/hooks/useBlockNumber'
import { useCallback, useMemo } from 'react'
import styled from 'styled-components/macro'
import { ExplorerDataType, getExplorerLink } from 'utils/getExplorerLink'

export default function PlaygroundControls() {
  const { chainId } = useWeb3React()
  const {
    aNewPlayground: aNewTenderlyForkProvider,
    playgroundProvider: tenderlyForkProvider,
    isPlayground,
    discardPlayground,
  } = useTenderlyPlayground()
  const selectChain = useSelectChain()
  const blockNumber = useBlockNumber()
  useSyncChainQuery()

  const createPlayground = useCallback(async () => {
    await aNewTenderlyForkProvider(chainId)
  }, [chainId, aNewTenderlyForkProvider])

  const blockExternalLinkHref = useMemo(() => {
    if (!chainId || !blockNumber) {
      return ''
    }

    if (tenderlyForkProvider) {
      return tenderlyForkProvider?.publicUrl || ''
    }

    return getExplorerLink(chainId, blockNumber.toString(), ExplorerDataType.BLOCK)
  }, [chainId, tenderlyForkProvider, blockNumber])

  const connectChain = useCallback(async () => {
    if (!tenderlyForkProvider) {
      return
    }
    await selectChain(Number.parseInt(tenderlyForkProvider.baseChainId))
    await discardPlayground()
  }, [discardPlayground, tenderlyForkProvider, selectChain])

  return (
    <ControlsPane>
      <Button href={blockExternalLinkHref}>Explorer</Button>
      {!isPlayground && <Button onClick={createPlayground}>Playground</Button>}
      {isPlayground && <Button onClick={createPlayground}>Clear Playground</Button>}
      {isPlayground && <Button onClick={connectChain}>Back To Network</Button>}
    </ControlsPane>
  )
}

const ControlsPane = styled.a`
  display: inline-flex;
  height: 70px;
  padding: 16px;
  align-items: center;
  gap: 24px;
  flex-shrink: 0;

  border-radius: 16px;
  border: 1px solid #e5e4ef;
  background: #fff;
  margin-top: 50px;
  position: absolute;
  bottom: 30px;
`

const Button = styled.a`
  display: flex;
  padding: 10px 24px;
  align-items: flex-start;
  border-radius: 8px;
  border: 1px solid #e4e3ee;
  background: #f5f6fc;
  box-shadow: 0px 1px 4px 0px rgba(23, 23, 24, 0.07);
  border-radius: 8px;
  border: 1px solid #e4e3ee;
  background: #f5f6fc;
  box-shadow: 0px 1px 4px 0px rgba(23, 23, 24, 0.07);
  color: #38363a;
  font-size: 14px;
  font-family: Inter;
  font-weight: 600;
  line-height: 20px;
  cursor: pointer;
  user-select: none;
  text-decoration: none;
`
```

### Step 4: Add the Playground Controls Componentn to the app

Finally, go to `App.tsx` and add the `PlaygroundsControl` component:

```diff
...
export default function App() {
...

  return (
    <ErrorBoundary>
...
      <BodyWrapper>
        <EnvironmentIndicator />
+       <PlaygroundControls />
...
			</BodyWrapper>
    </ErrorBoundary>
  )
}
```

### Step 5: Use the playground JSON RPC provider

Besides the basic setup shown in Steps 1-4, it’s necessary to ensure that switching from the public network to the fork is opaque for the registry of contracts, tokens, and other assets.

{% hint style="warning" %}
To make this tutorial work, we had to modify parts of the Uniswap codebase. We won’t be going too deep into the changes, but you can [check them out on GitHub](https://github.com/Tenderly/uniswap-playground-mode/commit/736745928dbe5b41f5f4ca61f48d65940ee5408c).

The following files were customized:

* constants/addresses.ts
* constants/chainInfo.ts
* constants/chains.ts
* constants/networks.ts
* constants/providers.ts
* constants/routing.ts
* constants/tokens.ts
{% endhint %}

In the Uniswap codebase, the `UNIVERSAL_ROUTER_ADDRESS` function looks up the address of the `UniversalRouter` based on the current chain. When switching from a chain to a fork (of that chain), the `UniversalRouter` is deployed at the same address on the forked chain.

In other words, the following must hold:

```tsx
UNIVERSAL_ROUTER_ADDRESS(1) 
	== UNIVERSAL_ROUTER_ADDRESS(`${TENDERLY_CHAIN_FORK_PREFIX}1`)
```

More generally, all lookups and calculations that are dependent on chain ID should yield the same results when done on a prefixed (forked) chain ID:

```tsx
calculation({chainId: 1}) 
	== calculation({chainId: `${TENDERLY_CHAIN_FORK_PREFIX}1`)
```

### Step 6: Run the app

To run the app, execute the following command:

```bash
yarn start
```

## Conclusion

In this tutorial, we used Tenderly Forks as the foundation for building a dapp playground that we integrated into Uniswap’s UI. The playground consists of a replica of the network the user wants to interact with. After this, we added the fork’s URL to MetaMask and set the balance on the account to an arbitrary value using our custom RPC call `tenderly_setBalance`.

This gave the user a simulated virtualized environment for dry-running transactions without the risk of losing real funds. Since the fork is a real-time replica of the latest state of the network, the user can be confident that the simulated results will always resemble real-world circumstances.
