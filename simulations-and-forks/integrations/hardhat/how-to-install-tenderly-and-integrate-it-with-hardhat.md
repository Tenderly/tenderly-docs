# How to install Tenderly and integrate it with Hardhat

Now that we have the Hardhat project all set up, it’s time to add Tenderly into the mix. We’ll be installing the **hardhat-tenderly** plugin and [the Tenderly CLI](https://github.com/tenderly/tenderly-cli#installation), which we’ll be using later:

```text
yarn add @tenderly/hardhat-tenderly
brew tap tenderly/tenderly
brew install tenderly
```

As you can see, we used **brew** to install Tenderly. You can find the [alternative installation steps here](https://github.com/tenderly/tenderly-cli#installation).

To let know Hardhat to load the Tenderly plugin, add the following line to your `hardhat.config.js`:

```text
require("@tenderly/hardhat-tenderly")
```

Next up, we can use the CLI to authenticate our development machine with our Tenderly dashboard \(if you don’t already have an account, [you can register here](https://dashboard.tenderly.co/register)\):

```text
tenderly login
✔ Email
✔ Enter your email: me@email.co
✔ Password: ************
```

To do the final configuration step, you’ll need to tell Hardhat which Tenderly project to connect with. You can do that by adding the following snippet of code into the `hardhat.config.js` `module.exports`:

```text
{
	tenderly: {
		username: "MyAwesomeUsername",
		project: "super-awesome-project"
	}
}
```

You can find the username and project by opening up [https://dashboard.tenderly.co](https://dashboard.tenderly.co/), and copying from the URL [_https://dashboard.tenderly.co/{**USERNAME**}/{**PROJECT**_](https://dashboard.tenderly.co/%7BUSERNAME%7D/%7BPROJECT)_}._ Alternatively, you can run `tenderly whoami` to get the needed information.

The Tenderly plugin is now good to go!

