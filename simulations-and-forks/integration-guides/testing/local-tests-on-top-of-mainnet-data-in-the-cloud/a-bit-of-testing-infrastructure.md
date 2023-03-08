---
description: >-
  Get a code snippet to quickly set up a Fork for testing and delete it after
  you're finished.
---

# A Bit of Testing Infrastructure

To reduce boilerplate in the rest of the examples, the `forkForTest` function encapsulates Tenderly API calls needed to create a Fork and delete it. It’s a bit more robust way to organize the test code that scales.&#x20;

Feel free to skip this code and go to usage examples.

{% hint style="info" %}
Tenderly creates 10 test addresses with 100 ETH for testing. By default, the ethers library does transaction signing with the 0th address as the default signer.
{% endhint %}

```tsx
import { JsonRpcProvider } from "@ethersproject/providers";
import axios, { AxiosResponse } from "axios";
import * as dotenv from "dotenv";
import { Signer } from "ethers";

dotenv.config();

// describes forking request. network_id is the only required attribute, 
// but feel free to override any
type TenderlyFork = {
    block_number?: number;
    network_id: string;
    initial_balance?: number;
    chain_config?: {
        chain_id: number;
    };
};

// All you need to access the forked environment from your tests
export type EthersOnTenderlyFork = {
    provider: JsonRpcProvider;
    /** test accounts: map from address to given address' balance */
    accounts: { [key: string]: string };
    /** test accounts: signers for transactions*/
    signers: Signer[],
    /** a function to remove fork from Tenderly infrastructure, meant for test clean-up */
    removeFork: () => Promise<AxiosResponse<any, any>>;
};

const anAxiosOnTenderly = () => axios.create({
    baseURL: "https://api.tenderly.co/api/v1",
    headers: {
        "X-Access-Key": process.env.TENDERLY_ACCESS_KEY || "",
        "Content-Type": "application/json",
    },
});
/**
    Create a fork on Tenderly with parameters declared through the 
    fork parameter.
*/
export const forkForTest = async (fork: TenderlyFork): Promise<EthersOnTenderlyFork> => {
    const projectUrl = `account/${process.env.TENDERLY_USER}/project/${process.env.TENDERLY_PROJECT}`;
    const axiosOnTenderly = anAxiosOnTenderly();

    const forkResponse = await axiosOnTenderly.post(`${projectUrl}/fork`, fork);
    const forkId = forkResponse.data.root_transaction.fork_id;
    console.info("Forked with fork id:", forkId)
    const provider = new JsonRpcProvider(`https://rpc.tenderly.co/fork/${forkId}`);

    const accounts = forkResponse.data.simulation_fork.accounts;

    const signers = Object.keys(accounts)
        .map(address => provider.getSigner(address));
    console.log("Accounts on fork", accounts)

    return {
        provider,
        accounts,
        signers,
        removeFork: async () => {
            console.log("Removing test fork", forkId);
            return await axiosOnTenderly.delete(`${projectUrl}/fork/${forkId}`);
        },
    };
};
```
