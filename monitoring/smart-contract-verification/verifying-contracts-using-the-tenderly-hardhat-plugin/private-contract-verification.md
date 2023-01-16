# Private Contract Verification

By default, the Tenderly Hardhat plugin performs public verification of Smart Contracts when using either automatic or manual approaches. When running private verification, the Smart Contract is verified within the project you specify.

## How to verify Smart Contracts privately

To enable private verification, the `tenderly` segment of Hardhat's configuration has to be extended by setting the `privateVerification` flag and [specifying your exact username and the project slug](https://docs.tenderly.co/other/platform-access/how-to-find-the-project-slug-username-and-organization-name) on Tenderly.

Add the following `tenderly` configuration property to your `hardhat.config.ts` and paste appropriate values instead of placeholders. There’s no need to change anything in your verification code.

```diff
// File: hardhat.config.ts
// –-snip–-
const config: HardhatUserConfig = {
  solidity: "0.8.17",
  networks: {
//    --snip—-
  },
+ tenderly: {
+   project: "project",
+   username: "username",
+   privateVerification: true,
+ },
};

export default config;
```

The `tenderly` section of the Hardhat user configuration consists of:

| Paramater           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| username            | <p>Username can be your own and the username of the organization. Which one, it depends on who is the owner of the project you are trying to verify your contracts on. If the project belongs to the organization you are part of, It should be filled with <code>organization username</code> , otherwise your own username.<br><br>The quickest and most secure way to make sure to which party the project belongs to is to look at the <code>url</code> of the particular project. You will see something like: <br><code>https://dashboard.tenderly.co/Tenderly/project/contracts</code><br>So you can take the username and project from there. In this case the username is <code>Tenderly</code> and the project is <code>project</code>.</p> |
| project             | Your project slug                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| privateVerification | Boolean. Default value: `false`.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |

To try it out, run any of the deployment scripts:

```bash
npx hardhat run scripts/greeter/automatic.ts --network ropsten
```

This configuration ensures all deployments run in the private mode until you change `hardhat.config.ts` again. To switch between public and private modes on a per-run basis, without hard-coding any specific mode in the project configuration, you need to externalize the configuration.

## How to externalize the configuration

In the case of [the example project on Git](https://github.com/Tenderly/hardhat-tenderly/tree/master/examples/contract-verification), some of the configuration is externalized using System Environment Variables.

Here’s one example of how the configuration references Environment Variables:

```tsx
// File: hardhat.config.ts
// --snip--
const automaticVerification = TENDERLY_AUTOMATIC_VERIFICATION === "true";
tdly.setup({ automaticVerifications: automaticVerification });
// --snip--
const config: HardhatUserConfig = {
// --snip--
  tenderly: {
    project: process.env.TENDERLY_PROJECT || "",
    username: process.env.TENDERLY_USERNAME || "",
    privateVerification: process.env.PRIVATE_VERIFICATION === "true",
  },
}
// --snip--
```

This allows you to parametrize Hardhat builds and verifications on a per-run basis. To run advanced manual verification, execute the following command in your terminal:

```
TENDERLY_PROJECT=myProject \
TENDERLY_USERNAME=myUsername \
npx hardhat run scripts/greeter/automatic.ts --network ropsten
```

If you’re using the `dotenv` package to expose System Environment Variables to JS, place your `TENDERLY_USERNAME` and `TENDERLY_PROJECT` into the `.env` file. This way, you don’t need to specify them explicitly when running the command as you’ll rarely change these parameters.
