---
description: >-
  Learn how to get API access by obtaining an API key and configuring your API
  client.
---

# Configuration of API Access

Besides using the all-in-one Tenderly development platform via the Dashboard, you can interact with our features via Tenderly API. Use the API when you need to programmatically create a Fork, retrieve all Forks you created in your project, run simulation bundles, simulate the execution of an arbitrary transaction, and more.

## Get an API key

To get your Access Token, go to [**Settings > Authorization**](https://dashboard.tenderly.co/account/authorization) and click **Create Access Token**. If you want to create an organization token, you can do so from your [organization’s settings page](https://dashboard.tenderly.co/organizations).

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

With Tenderly API, you can either do operations that are related to your particular project or a specific Fork. In these cases, you need to specify your project’s slug and the user: `TENDERLY_USER` and `TENDERLY_PROJECT`.&#x20;

You can extract it from the Dashboard URL and place these in a safe place:

`https://dashboard.tenderly.co/account/TENDERLY_USER/project/TENDERLY_PROJECT/`

Here's an example of usage:

```tsx
const { TENDERLY_USER, TENDERLY_PROJECT } = process.env
const tAxios = anAxiosOnTenderly();
const projectBase = `account/${TENDERLY_USER}/project/${TENDERLY_PROJECT}`;
const resp = await tAxios.get(`${projectBase}/simulations`);

console.log(resp.data)
```

### Example of the `.env` file

By this time, your .`env` file (at the root of your npm project) holds these three items:

```bash
TENDERLY_PROJECT=...
TENDERLY_USER=...
TENDERLY_ACCESS_KEY=...
```
