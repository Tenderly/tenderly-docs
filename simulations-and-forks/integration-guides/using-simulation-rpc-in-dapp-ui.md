---
description: >-
  Learn about the benefits of integrating transaction simulations into your dapp
  via Simulation RPC. Follow the example of integrating the Simulation RPC into
  Uniswap's UI.
---

# Using Simulation RPC in Dapp UI

You can introduce simulations into your dapp by integrating Simulation RPC or Simulation API. This way, you can:

1. Dry-run users' transactions before they sign and submit them on-chain.
2. Provide better visibility into potential rollbacks and avoid losing money on gas fees.
3. Provide better visibility into the outcomes of successful apps, including moving assets and state changes relevant to the user.
4. Build logic around simulation results to show users whether their transactions bring optimal value and suggest improvements.&#x20;

Here are a few examples:&#x20;

* If you're building a wallet-like app, you can show how a transaction moves ERC-20 tokens and enable users to see the shifting of their funds.
* If you're building a DeFi product, you can use events to analyze whether a transaction meets the optimal conditions set by the user in the UI.
* If you're preparing a governance proposal, consisting of several transactions, you can do a simulation bundle to see how the proposal is applied.\
  You can even bundle the proposal transactions with several test transactions to verify that your proposal executes as intended and identify possible blind spots.

In this example, we'll show how to integrate Simulation RPC into the Uniswap UI and show the exact token hops along the exchange path. This way, we'll give the user higher visibility into the effects of the transaction and allow them to make a well-informed decision on whether or not to proceed.



## The `Simulation` component requirements

Here are the requirements for the simulation component:

* The component should display the number of tokens the user has before and after signing and sending the transaction.
* The simulation should be done every time the trade data changes, so it needs to receive the `trade` and `allowedSlippage` parameters.&#x20;
* The component must keep track of:
  * Current balances (before the swap).
  * The `Swap` event we'll use to calculate the new balances.
  * An array of `Transfer` events we'll use to calculate the new balances.

## Render the `Simulation` into `ConfirmSwapModal`

The best place to inform the user about the outcomes of a transaction is `ConfirmSwapModal`, just before they can sign and send the transaction.

The code is redacted for brevity:

```diff
export default function ConfirmSwapModal({
  /* ... */
}: {
  /* ... */
}) {
  // ...
  const modalHeader = useCallback(() => {
    return trade ? (
      <>
        <SwapModalHeader.../>
+        <Simulation trade={trade} recipient={null} allowedSlippage={allowedSlippage} />
      </>
    ) : null
  }, [/* ... */])
  //...

```

## The `Simulation` component implementation

The logic of the component lies in the **simulate** function:

* It runs in event of changing `trade` or `provider` arguments, so it updates and re-simulates whenever the swap potentially changes.
* It calls `setOldBalances`, which gets the balances of In and Out ERC-20 tokens and stores them in the `oldBalances` state variable.
* It calls `simulateRPC`, which performs the Simulation RPC call to `tenderly_simulateTranscation` and then:
  * It parses through decoded logs to find the `Transfer` events and stores them in the component's `transfers` state variable.
  * It parses through the decoded logs to find the `Swap` event and stores it in the component's `swap` state variable.

Finally, to render the simulation results, we display the `SimulationDetails` component, which is a purely functional component. It calculates the old and new states and renders the data based on `trade`, `swap`, `transfers`, and `oldBalances`.

```tsx
const Simulation = ({
  trade,
  allowedSlippage,
  recipient
}: {
  trade: InterfaceTrade<Currency, Currency, TradeType> | undefined;
  recipient: string | null;
  allowedSlippage: Percent;
}) => {
  const { account, provider } = useWeb3React();
  const nativeCurrency = useNativeCurrency();

  const deadline = useTransactionDeadline();
  const signatureData = useERC20PermitFromTrade(trade, allowedSlippage, deadline);
  const args = useSwapCallArguments(
    trade,
    allowedSlippage,
    recipient,
    signatureData.signatureData,
    deadline,
    undefined
  );

  const [oldBalances, setOldBalances] = useState<any[]>([]);
  const [transfers, setTransfers] = useState<any[]>([]);
  const [swap, setSwap] = useState<any>({});

  useEffect(() => {
    onSimulate();
  }, [trade, provider]);

  async function onSimulate() {
    setOldBalances([]);
    setSwap({});
    const { address, calldata, value } = args[0];
    const provider = RPC_PROVIDERS[SupportedChainId.MAINNET];

    await getCurrentBalances();
    await simulateRPC(account, address, calldata, value);
  }

  async function getCurrentBalances() {
    return Promise.all([
      provider.send('eth_getBalance', [account, 'latest']),
      provider.send('eth_call', [
        {
          to: '0x1f9840a85d5aF5bf1D1762F925BDADdC4201F984',
          data: `0x70a0823100000000000000000000000000${stripX(account)}`
        },
        'latest'
      ])
    ]).then((oldBalances) => {
      setOldBalances(oldBalances);
    });
  }

  async function simulateRPC(account: string, address: string, calldata: string, value: string) {
    RPC_PROVIDERS[SupportedChainId.MAINNET]
      .send('tenderly_simulateTransaction', [
        {
          from: account,
          to: address,
          data: calldata,
          value: stripHexZero(value)
        },
        'latest', // block number to simulate on
        null // optional state overrides for involved contracts
      ])
      .then((simulationResponse) => {
        console.log('Simulation Response', simulationResponse);
        setTransfers(simulationResponse.logs.filter((log: any) => log.name === 'Transfer'));
        setSwap(simulationResponse.logs.filter((log: any) => log.name === 'Swap')[0]);
      });
  }

  return (
    <>
      ...
      <SimulationDetails
        trade={trade}
        syncing={oldBalances.length == 0 && transfers.length == 0 && !!swap.inputs}
        transfers={transfers}
        oldBalances={oldBalances}
        swap={swap}
      />
    </>
  );
};
```
