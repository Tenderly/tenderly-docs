# Configuration of API access

Besides using the Tenderly platform via Dashboard, you can also interact with all of our services via Tenderly API. You’ll want to use the API when you need to do things such as programmatically creating a Fork, retrieving all Forks you have created in your project, running Simulation batches and so on, or perhaps simulate the execution of an arbitrary transaction.

## Get an API key

To get your Access Token, go to the [**Settings > Authorization**](https://dashboard.tenderly.co/account/authorization) and click on **Create Access Token**. If you want to create an organization token you can do so from your [organization’s settings page](https://dashboard.tenderly.co/organizations).

The token you get will be used in API authentication.

{% hint style="warning" %}
Do not share the API Access token freely.
{% endhint %}

## Configure your API client

The token must be sent via `X-Access-Key` HTTP header.

Here’s an example of configuring Axios to work with Tenderly, assuming you’ll use `dotenv` to store your secrets.

```tsx
import axios from "axios";
import * as dotenv from "dotenv";

dotenv.config();

export const anAxiosOnTenderly = () =>
  axios.create({
      baseURL: "https://api.tenderly.co/api/v1",
      headers: {
          "X-Access-Key": process.env.TENDERLY_ACCESS_KEY || "",
          "Content-Type": "application/json",
      },
  });
```

### Project-related operations

With Tenderly API you can either do operations that are related to your particular project or a specific Fork. In this case, you’ll also need to specify your project’s slug and the user: `TENDERLY_USER` and `TENDERLY_PROJECT`.&#x20;

You can extract it from the dashboard URL and place these in a safe place:

`https://dashboard.tenderly.co/TENDERLY_USER/TENDERLY_PROJECT/`

And the example of usage:

```tsx
const { TENDERLY_USER, TENDERLY_PROJECT } = process.env
const tAxios = anAxiosOnTenderly();
const projectBase = `account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}`;
const resp = await tAxios.get(`${projectBase}/simulations`);

console.log(resp.data)
```

### Example of the `.env` file

By this time your `env` file holds these 3 items:

```bash
TENDERLY_PROJECT=...
TENDERLY_USER=...
TENDERLY_ACCESS_KEY=...
```
