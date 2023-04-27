---
description: >-
  Learn how to use Web3 Actions as a serverless backend to respond to relevant
  events. Follow a Tic-Tac-Toe example to set up a Web3 Action that will monitor
  game changes.
---

# How to Handle On-Chain Events

This tutorial will teach you how to **create a serverless backend for your smart contract using Tenderly Web3 Actions**. Web3 Actions allow you to run custom code in response to on-chain or off-chain events that are initiated by your smart contract.

To illustrate how Web3 Actions work, we will build a simple Tic-Tac-Toe game and deploy it to a test network. The smart contract will be responsible for maintaining the game state while Web3 Actions will be used to monitor changes to the game.

**Whenever a specific event gets fired from the smart contract, Tenderly will execute your custom code in the form of a NodeJS project**. The results of the game and the game board will be printed to the console each time a player makes a move or when the game is over.

{% hint style="success" %}
Check out this [Github repo](https://github.com/Tenderly/examples-web3-actions/) to find the source code for this project. Feel free to clone the repo and play around with it, or code along.
{% endhint %}

## Understanding Web3 Actions

Smart contracts allow you to execute custom code when an event is triggered, a function is invoked, or perhaps periodically.

Tenderly helps you streamline this process with Web3 Actions. You can write your Web3 Actions in a single Javascript file or deploy them as a NodeJS project.

**Web3 Actions also allow you to perform any action you normally would with NodeJS**. This tutorial will show you how to use the Tenderly CLI to deploy your Web3 Actions and ensure they run when specific conditions are met.

{% hint style="info" %}
Learn more about Web3 Actions and explore how you can use them in your projects with [**Basics of Web3 Actions**](broken-reference).
{% endhint %}

### Project Overview

The purpose of this project is to show you how to deploy a smart contract and write several Javascript functions that Tenderly will invoke when an event occurs. You will learn how to use the Tenderly CLI to deploy your Web3 Actions to Tenderly’s infrastructure.

Here’s a step-by-step overview of how we will go about doing this:

1. Deploy the smart contract to a test network
2. Use the Tenderly CLI to set up Javascript and config files needed to run the Web3 Actions
3. Develop functions that respond to game events
4. Deploy those functions to Tenderly’s infrastructure using the CLI

{% hint style="warning" %}
For this tutorial, you’ll need access to the **Tenderly Dashboard**. If you don’t have an account, [**sign up here for free**](https://dashboard.tenderly.co/register?utm\_source=homepage) (no cc required as well).
{% endhint %}

## 0: Deploy the smart contract

{% hint style="info" %}
If you’re coding along, you can skip this step and use the contract we [**deployed and verified in Tenderly**](https://dashboard.tenderly.co/contract/ropsten/0x1eb7dbd296eb3fc08b2b6217d87e6bf3cb6e42df).
{% endhint %}

We will use a pre-written smart contract. Check out the source code of the[ **smart contract on GitHub**](https://github.com/Tenderly/examples-web3-actions/blob/main/tic-tac-toe/TicTacToe.sol). This smart contract is designed to emit events whenever a change to the state of the game occurs.

Our simple Tic-Tac-Toe game can have four possible states:

* Game start
* Player joins the game
* Player makes a move
* Game over

### Prerequisite

**Create Two Accounts** - deploy the smart contract to any [network that is supported by Tenderly](https://docs.tenderly.co/supported-networks-and-languages). The most convenient way to do this is with [Remix](https://remix.ethereum.org/) and the [Metamask](https://metamask.io/) wallet plugin. You need two accounts that have a positive Ether balance. These accounts will represent the two players. For the purpose of this tutorial we will use Sepolia. If you plan to follow along with this tutorial, you can use the [Sepolia faucet](https://sepoliafaucet.com/) to add Ether to the accounts.

**Compile the contract -** use the Remix IDE to compile the smart contract. Create a new contract file and add the code found [**here**](https://github.com/Tenderly/examples-web3-actions/blob/main/tic-tac-toe/TicTacToe.sol).

<figure><img src="../../.gitbook/assets/image (69).png" alt="Compiling the contract in the Remix IDE"><figcaption><p>Compiling the contract in the Remix IDE</p></figcaption></figure>

**Deploy to a test network** - in your Metamask browser plugin, make sure Ropsten is selected as your preferred network. Next, go to the **“Deploy And Run Transactions”** section in Remix and select **`Injected Provider`**. Click **“Deploy”** once you’ve made sure that the account references the account in Metamask.

<figure><img src="../../.gitbook/assets/image (73).png" alt="Deploying the contract to a testnet"><figcaption><p>Deploying the contract to a testnet</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (92).png" alt="Copying the contract address"><figcaption><p>Copying the contract address</p></figcaption></figure>

To get more information on the deployed contract, check out the **“Deployed Contracts”** section. Click the copy icon to copy the full contract address (<mark style="color:orange;">`0x1EB...`</mark>) and store it somewhere because we’ll need it for the steps that follow.

Now go to the **Tenderly Dashboard to verify the contract**. This will make it possible for us to interact with the contract later on in the tutorial.

## 1: Set Up Web3 Actions via the Tenderly CLI

To continue with this tutorial, you need to have the **Tenderly CLI** installed on your machine. Follow [**this guide**](https://github.com/Tenderly/tenderly-cli#installation) to learn how to set it up and authenticate access.

With the CLI installed, create a new directory and <mark style="color:orange;">`cd`</mark> into it. Initialize your Web3 Actions by running the <mark style="color:orange;">`tenderly actions`</mark>` ``init` command:

```
$> cd tdly-actions
$> tenderly actions init
```

You'll be prompted to select one of your existing Tenderly projects. Your Web3 Actions will be deployed to this project and should appear in your directory structure like so:

```bash
$> ls actions
  example.ts     # where we write Web3 actions code
  tsconfig.json
  package.json
```

Typescript is the default language but you can switch to plain Javascript. Before you execute the init command, set Javascript as your preferred language like so: <mark style="color:orange;">`tenderly actions init --language javascript`</mark>.

{% hint style="info" %}
The `package.json` holds npm dependencies which will be available when you deploy your Web3 Action. The <mark style="color:orange;">`tsconfig.json`</mark> file holds Typescript configuration related only to <mark style="color:orange;">`.ts`</mark> files within the <mark style="color:orange;">`actions`</mark> directory.
{% endhint %}

### 1.1. Add Tic-Tac-Toe Contract’s ABI

Before we dive deeper into the code, copy the ABI generated by the compiler to the actions directory. In our example, this is the <mark style="color:orange;">`tdly-actions`</mark> directory.

In Remix, go to <mark style="color:orange;">`files/artifacts/TicTacToe.json`</mark>, copy/paste the file contents and paste them into your project’s <mark style="color:orange;">`TicTacToe.json`</mark> file.

{% hint style="danger" %}
All files your Web3 Action code uses and references must be placed in the <mark style="color:orange;">`actions`</mark> directory (e.g. <mark style="color:orange;">`TicTacToe.json`</mark>).
{% endhint %}

### 1.2. Configure Typescript to Import a JSON File as a Module

By default, Typescript doesn’t allow you to import JSON files as modules. You need to configure Typescript to be able to import the <mark style="color:orange;">`TicTacToe.json`</mark> file as a module and access it as an object.

Go to your <mark style="color:orange;">`tsconfig.json`</mark> file and include the following two configurations under the <mark style="color:orange;">`compilerOptions`</mark> entry:

```diff
{
    ...
    "compilerOptions": {
	...
+        "resolveJsonModule": true,
+        "esModuleInterop": true
    },
   ...
}
```

## 2: Write a Function to Handle New Game Event

Write a function that will execute when a new game is started. Let’s rename the Typescript file to something more descriptive:

```bash
mv example.ts ticTacToeActions.ts
```

To harness the power of Typescript, we'll first need to define a type representing the game state. In essence, we'll store a replica of the game state in the storage of your Web3 Action. Each field contains the ID of the player who played there. We'll map the player's address to their turn (first, second, etc) in the <mark style="color:orange;">`players`</mark> object.

### 2.1. Add an Action

```typescript
// ticTacToeActions.ts
import {
 ActionFn,
 Context,
 Event,
 TransactionEvent
} from '@tenderly/actions';
import { ethers } from "ethers";
import TicTacToe from "./TicTacToe.json";

export type Game = {
 players: { [address: string]: number };
 board: number[][];
}
```

At this point, we are ready to define the actual Web3 Action like so:

```typescript
// ticTacToeActions.ts continued 
export const newGameAction: ActionFn = async (
    context: Context,
    event: Event
) => {
    let txEvent = event as TransactionEvent;

    let iface = new ethers.utils.Interface(TicTacToe.abi);

    const result = iface.decodeEventLog(
        "GameCreated",
        txEvent.logs[0].data,
        txEvent.logs[0].topics
    );

    const { gameId, playerNumber, player } = result;

    console.log("Game Created Event:", {
        gameId: gameId.toString(),
        playerNumber,
        player,
    });

    const game: Game = createNewGame();
    await context.storage.putJson(gameId.toString(), game);
};
```

This Web3 Action will handle the <mark style="color:orange;">`GameCreated`</mark> event that is defined in the smart contract.

Looking at the smart contract, we can see that only one event is getting fired from the <mark style="color:orange;">`newGame`</mark> function, so we’re interested in the first log entry. We can get the <mark style="color:orange;">`result`</mark> with ethers.js by decoding <mark style="color:orange;">`txEvent.logs[0].data`</mark> of the GameCreated event, based on the <mark style="color:orange;">`TicTacToe.abi`</mark>.

Here we can access the ID associated with this particular game once it has been created: <mark style="color:orange;">`result.gameId`</mark>. We want to track the data for this particular game: players and moves they made, using a brand new <mark style="color:orange;">`Game`</mark> instance. We’re saving the object representing the new game in the Storage with this command: <mark style="color:orange;">`context.storage.putJson(gameId, game)`</mark>.

With an empty board, we are setting the foundation to persist future changes which are handled by other actions.

You may also write automated tests to verify the behaviour of the Web3 Action. Some tests are available in the repository, but this is out of the scope of this tutorial.

### 2.2. Specify New Game Action Invocation

Open up tenderly.yaml. In the <mark style="color:orange;">`specs`</mark> section, define the specs for <mark style="color:orange;">`newGame`</mark> (arbitrary name) to invoke the function <mark style="color:orange;">`newGameAction`</mark>. You can do so like this <mark style="color:orange;">`newGameAction:newGameAction`</mark> — first we define the name of the file containing the function and then the function name.

Next, specify the <mark style="color:orange;">`trigger`</mark> that Tenderly is supposed to watch out for to invoke the action. This is a <mark style="color:orange;">`transaction`</mark> trigger that will run when the block is mined. We’re doing this for <mark style="color:orange;">`network 3`</mark> when the event <mark style="color:orange;">`NewGame`</mark> is emitted from the contract on the specified address.

Replace <mark style="color:orange;">`TTT_CONTRACT_ADDRESS`</mark> with the actual address of your smart contract. If you want to deploy the contract to a network other than Ropsten, specify the network’s ID as the value of the network.

{% hint style="info" %}
Replace <mark style="color:orange;">`YOUR_USERNAME`</mark> and <mark style="color:orange;">`YOUR_PROJECT_SLUG`</mark> with your Tenderly username and the slug of your project. You can copy those from the Dashboard URL: <mark style="color:orange;">`https://dashboard.tenderly.co/{YOUR_USERNAME}/{YOUR_PROJECT_SLUG}/transactions`</mark>
{% endhint %}

```yaml
account_id: ""
actions:
  YOUR_USERNAME/YOUR_PROJECT_SLUG:
    runtime: v1
    sources: actions
    specs:
      newGame:
        description: Respond to newGame event
        function: ticTacToeActions:newGameAction
        trigger:
          type: transaction
          transaction:
            status:
              - mined
            filters:
              - network: 3
                eventEmitted:
                  contract:
                    address: TTT_CONTRACT_ADDRESS
                  name: GameCreated
project_slug: ""
```

### 2.3. Verify Your Tic-Tac-Toe Smart Contract on Tenderly

Before deploying the contract, you need to verify it in your Tenderly Dashboard. Follow this guide to learn [**How to Add a Contract to a Tenderly Project**](https://docs.tenderly.co/monitoring/smart-contracts#adding-a-contract-to-your-project-via-tenderly-cli).

If you wish, you can upload the contract through your browser. Once uploaded, select the TicTacToe contract, the network you deployed it to, and the contract address.

Click Add Contract and fill out the compiler options as shown in the picture below:

<figure><img src="../../.gitbook/assets/image (74).png" alt="Verifying and adding the contract to Tenderly "><figcaption><p>Verifying and adding the contract to Tenderly </p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (87).png" alt="Adding the contract compiler information "><figcaption><p>Adding the contract compiler information </p></figcaption></figure>

### 2.4. Deploy the Web3 Action to Tenderly

To deploy your Web3 Action, execute the <mark style="color:orange;">`deploy`</mark> command using the Tenderly CLI:

```bash
tenderly actions deploy
```

The output should look like this:

<figure><img src="../../.gitbook/assets/image (79).png" alt="The Web3 Action execution output"><figcaption><p>The Web3 Action execution output</p></figcaption></figure>

To see details about the deployment of your Web3 Action, check the Tenderly Dashboard. If the deployment was successful, you should see something like this:

<figure><img src="../../.gitbook/assets/image (80).png" alt="Opening the Web3 Action deployment information "><figcaption><p>Opening the Web3 Action deployment information </p></figcaption></figure>

### 2.5. Try Joining a New Game 🎉

To verify that everything is working properly, head back to Remix and create a new game or even several games.

Open up the TicTacToe contract and hit <mark style="color:orange;">`newGame`</mark>. Metamask should prompt you to confirm the execution of the Web3 Action.

Once the transaction is submitted to the chain, Remix should produce an output similar to this:

<figure><img src="../../.gitbook/assets/image (96).png" alt="Creating a new game in Remix"><figcaption><p>Creating a new game in Remix</p></figcaption></figure>

Next, head back to your Tenderly Dashboard and open the Transactions section to see your transaction. In the Actions section, you’ll notice that the **“Latest Execution”** column has changed.

To view the execution history, open your Web3 Action and click the Execution History tab:

<figure><img src="../../.gitbook/assets/image (81).png" alt="Opening the Execution history tab for your Web3 Action "><figcaption><p>Opening the Execution history tab for your Web3 Action </p></figcaption></figure>

The execution history will provide you with the following data:

<figure><img src="../../.gitbook/assets/image (89).png" alt="The execution history data"><figcaption><p>The execution history data</p></figcaption></figure>

In the upper pane, you'll find information about the payload coming from the chain. The lower pane contains details about the logged game number. In our case, this is <mark style="color:orange;">`0xb`</mark>, which means it’s the 11th game started for this contract.

### 2.6. Check the Storage of Your Web 3 Actions

Click the **“Go To Storage”** button to see the contents of the Storage. Each game that is initiated will get its own storage slot in this key-value map.

When you open the game we just created with the **ID 11**, you’ll see zeros across all the fields, meaning no players have played the game yet.

<figure><img src="../../.gitbook/assets/image (90).png" alt="Opening the Storage of your Web3 Action "><figcaption><p>Opening the Storage of your Web3 Action </p></figcaption></figure>

## 3: Add a Web3 Action to Handle New Players Joining a Game

The player joining the game should be processed by registering the address of the player and their move (1 or 2).

Besides the boilerplate code that helps us retrieve the event data, the <mark style="color:orange;">`playerJoinAction.ts`</mark> file also contains the code that allows us to:

* Read the current game state from the storage using the game’s ID (<mark style="color:orange;">`storage.getJson`</mark>).
* Retrieve the player’s address and store their turn: <mark style="color:orange;">`game.players[player] = playerNumber`</mark>
* Save the updated game object to the storage of Web3 Action using <mark style="color:orange;">`storage.putJson`</mark>.

```typescript
// playerJoinAction.ts

export const playerJoinedAction: ActionFn = async (
    context: Context,
    event: Event
) => {
    let txEvent = event as TransactionEvent;
    let iface = new ethers.utils.Interface(TicTacToe.abi);
    const result = iface.decodeEventLog(
        "PlayerJoinedGame",
        txEvent.logs[0].data,
        txEvent.logs[0].topics
    );

    const gameId = result.gameId.toString();
    const playerAddress = result.player.toLowerCase() as string;
    const playerNumber = result.playerNumber;

    console.log("Player joined event:", {
        gameId,
        playerAddress,
        playerNumber,
    });

    const game: Game = (await context.storage.getJson(gameId)) as Game;
    game.players[playerAddress] = playerNumber;

    await context.storage.putJson(result.gameId.toString(), game);
};
```

### 3.1. Specify PlayerJoinedGame Action Invocation

We also need to extend the <mark style="color:orange;">`specs`</mark> from the <mark style="color:orange;">`tenderly.yaml`</mark> file to include the specifications needed to invoke the Web3 Action.

```yaml
playerJoined:
        description: Respond to player joining game
        function: ticTacToeActions:playerJoinedAction
        trigger:
          type: transaction
          transaction:
            status:
              - mined
            filters:
              - network: 3
                eventEmitted:
                  contract:
                    address: TTT_CONTRACT_ADDRESS
                  name: PlayerJoinedGame
```

### 3.2. Deploy the action to Tenderly

Deploy your Web3 Action by running the <mark style="color:orange;">`deploy`</mark> command. This command will also redeploy previously deployed Web3 Actions.

```javascript
tenderly action deploy
```

### 3.3. Try Joining a New Game

Join a new game by going over to Remix and adding the game number from the logs in the <mark style="color:orange;">`newGame`</mark> input field. To submit the transaction, click the <mark style="color:orange;">`joinGame`</mark> button:

<figure><img src="../../.gitbook/assets/image (85).png" alt="Joining a new game in Remix "><figcaption><p>Joining a new game in Remix </p></figcaption></figure>

Once the transaction has been mined, the logs of the execution will display <mark style="color:orange;">`playerNumber: 1`</mark>.

<figure><img src="../../.gitbook/assets/image (93).png" alt="The execution log"><figcaption><p>The execution log</p></figcaption></figure>

To play the game, switch to your other account in Metamask and click <mark style="color:orange;">`joinGame`</mark> again. Upon the completion of the transaction, you’ll see a similar log output in the Execution History.

### 3.4. Check the Storage of Your Web 3 Actions

<figure><img src="../../.gitbook/assets/image (94).png" alt="Opening the execution of your Web3 Action"><figcaption><p>Opening the execution of your Web3 Action</p></figcaption></figure>

Open any of these executions and click the **“Go To Storage”** button.

The game our players have joined has the ID of 11, and this is the state before any move has been made. The Tic-Tac-Toe board contains only zeros and the map from an Ethereum address to the player’s turn is present.

<figure><img src="../../.gitbook/assets/image (91).png" alt="Opening the Storage key value "><figcaption><p>Opening the Storage key value </p></figcaption></figure>

### 3.5. Add an Action to Handle When Player Makes a Move

Using Ethers, we get the game ID and load the game instance from storage. Next, update the field in row <mark style="color:orange;">`result.boardRow`</mark> and column <mark style="color:orange;">`result.boardCol`</mark> with the player’s input <mark style="color:orange;">`game.players[player]`</mark>**.**

The function <mark style="color:orange;">`processNewGameState`</mark>, will log the board to the console, but you can also send a tweet when a move is made, trigger a new transaction on the chain, or use it in any other way.

```typescript
// ticTacToeActions.ts 
//...
export const playerMadeMoveAction: ActionFn = async (
    context: Context,
    event: Event
) => {
    let txEvent = event as TransactionEvent;
    let iface = new ethers.utils.Interface(TicTacToe.abi);
    const result = iface.decodeEventLog(
        "PlayerMadeMove",
        txEvent.logs[0].data,
        txEvent.logs[0].topics
    );

    const gameId = result.gameId.toString();
    const game = (await context.storage.getJson(gameId)) as Game;
    const player = result.player.toLowerCase() as string;
    const { boardRow, boardCol } = result;

    console.log("Player's move event log:", {
        gameId,
        player,
        boardRow: boardRow.toString(),
        boardCol: boardCol.toString(),
    });

    console.log(
        `Move: gameId ${gameId}, game ${JSON.stringify(
            game
        )}, boradRow ${boardRow}, boardCol ${boardCol}, player ${player}`
    );

    game.board[boardRow][boardCol] = game.players[player];
    console.log("MV", JSON.stringify(game));
    await context.storage.putJson(gameId, game);

    processNewGameState(game);
};

const processNewGameState = (game: Game) => {
    let board = "\n";
    game.board.forEach((row) => {
	row.forEach((field) => {
		if (field == 1) {
		    board += "❎ ";
		    return;
		}

		if (field == 2) {
		    board += "🅾️ ";
		    return;
		}

		board += "💜 ";
	});

	board += "\n";
    });

    console.log(board);
}
```

The corresponding spec for this action is:

```yaml
playerMadeMove:
        description: Respond to player making a move event
        function: ticTacToeActions:playerMadeMoveAction
        trigger:
          type: transaction
          transaction:
            status:
              - mined
            filters:
              - network: 3
                eventEmitted:
                  contract:
                    address: TTT_CONTRACT_ADDRESS
                  name: PlayerMadeMove
```

### 3.6. Make a Move to Play the Game

To make a move, use Metamask to switch to the first player who joined the game. Next, enter the game number you received, as well as the row and column on the board (0, 1).

<figure><img src="../../.gitbook/assets/image (88).png" alt="Making a move in Remix "><figcaption><p>Making a move in Remix </p></figcaption></figure>

When the action gets executed, the output should look like this:

<figure><img src="../../.gitbook/assets/image (95).png" alt="The Web3 Action execution output"><figcaption><p>The Web3 Action execution output</p></figcaption></figure>

## Step 4. Add a Web3 Action to Handle When the Game is Over

Below you’ll find the code for the <mark style="color:orange;">`GameOver`</mark> event. The <mark style="color:orange;">`GameOver`</mark> event is fired when a player makes a move that wins the game or when the board is full. This event is fired after the <mark style="color:orange;">`PlayerMadeMove`</mark> event. In the <mark style="color:orange;">`txEvent.logs`</mark> list, the <mark style="color:orange;">`GameOver`</mark> event is the second element.

An easy way to get <mark style="color:orange;">`GameOver`</mark> event is to access it via the <mark style="color:orange;">`txEvent.logs[1]`</mark>. However, we’ll implement a more robust solution which doesn’t depend on the order and number of events fired.

First, you need to get the <mark style="color:orange;">`gameOverTopic`</mark> using ethers via <mark style="color:orange;">`iface.getEventTopics`</mark>. This will give you the corresponding hexadecimal value. Next, you need to find the log entry in the <mark style="color:orange;">`txEvent.logs`</mark>, whose topics list contains the <mark style="color:orange;">`gameOverTopic`</mark>. This is our <mark style="color:orange;">`GameOver`</mark> event log that we can decode using Ethers.

```javascript
export const gameOverAction: ActionFn = async (context: Context, event: Event) => {
	let txEvent = event as TransactionEvent;
	let iface = new ethers.utils.Interface(TicTacToe.abi);

	const gameOverTopic = iface.getEventTopic("GameOver");
	const gameOverLog = txEvent.logs.find(log => log.topics.find(topic => topic == gameOverTopic) !== undefined);

	if (gameOverLog == undefined) {
		// impossible
		throw Error("GameOver log not found in event's logs");
	}

	const result = iface.decodeEventLog("GameOver", gameOverLog.data, gameOverLog.topics);

	console.log(result);

	const gameId = result.gameId.toString();
	const winner = result.winner as number;

	const winnerMessage = getWinnerMessage(winner);
	if (winnerMessage !== false) {
		console.info(`🎉 Winner of the game ${gameId} is ${winnerMessage}`);
	} else {
		console.error("🤔 Weird winner code");
	}
}
```

### 4.1. Specify GameOver Action Invocation

Finally, we need to add the specification to invoke the <mark style="color:orange;">`GameOver`</mark> action by extending the <mark style="color:orange;">`specs`</mark> in <mark style="color:orange;">`tenderly.yaml`</mark>:

```yaml
gameOver:
        description: Respond to game over
        function: ticTacToeActions:gameOverAction
        trigger:
          type: transaction
          transaction:
            status:
              - mined
            filters:
              - network: 3
                eventEmitted:
                  contract:
                    address: TTT_CONTRACT_ADDRESS
                  name: GameOver
```

### 4.2. Play the Game

Keep playing until one player wins the game or the board is entirely filled out. At the end of the game, the Execution History should look like this:

<figure><img src="../../.gitbook/assets/image (78).png" alt="The execution history at the end of the game"><figcaption><p>The execution history at the end of the game</p></figcaption></figure>
