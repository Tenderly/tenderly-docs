# How to Generate API Access Tokens

This guide shows you how to generate access tokens to authenticate access to the [**Tenderly API**](https://docs-api.tenderly.co/) and [**Hardhat Plugin**](https://github.com/Tenderly/hardhat-tenderly).

To proceed, you need to have a Tenderly account. If you don’t have one already, register for a free account on the [**signup page**](https://dashboard.tenderly.co/register).

## Generate an API access token for a personal account

Follow the steps below to generate an access token for the API for your personal account.

* Open up your **Tenderly Dashboard.**
* Click on your profile photo from the top nav bar.
* From the dropdown, click on **Settings**.
* Next, navigate to the **Authorization** tab.
* Click the **General Access Token** button.
* Give your new access tokens a descriptive label to keep things organized.

This is helpful if you need to generate multiple API access tokens for use in different places.

* Click **Generate**.

You will be prompted to copy your private key. For security reasons, the private key will be displayed only once during the initial creation. Copy your private key and store it in a safe place.

* Once you’ve copied the private key, click **Okay, close.**

![Generating a personal access token](../../.gitbook/assets/API\_prersonal\_account)

## Generate an API access token for an organization

To generate an API access token for an organization, you first need to create one or be part of one. Follow this tutorial to learn [how to set up an organization](https://docs.tenderly.co/teams-and-collaboration#organizations).

💡 API access tokens created within an organization can be accessed and managed by all of its members who have appropriate privileges.

* Open up your **Tenderly Dashboard**.
* Click on your profile photo from the top nav bar.
* From the dropdown, click on **Organizations**.
* Click on the organization where you want to generate access tokens.
* In the left-hand sidebar, click on **Access Tokens**.

This is where all the API access tokens from your organization will be listed.

* To create a new access token, click on **New Access Token.**
* Give the token a descriptive label to keep things organized.
* Click **Generate**.

You will be prompted to copy your private key. For security reasons, the private key will be displayed only once during the initial creation. Copy your private key and store it in a safe place.

* Once you’ve copied the private key, click **Okay, close.**

![Generating an organization access token](../../.gitbook/assets/Organization\_API)

## Remove an API access token

Removing an API access token and revoking access to it will disable all endpoints and third-party services that are using the access token.

### Personal accounts

Go to **Profile** > **Settings** > **Authenticate** to locate your access tokens.

Click on the **Revoke Access Token** button next to the token you want to remove.

Confirm your action by clicking the **Revoke Access Token** button.

### Organizations

Go to **Profile** > **Organizations** > **\[Organization name]** > **Access Tokens**.

Click on the **Revoke Access Token** button next to the token you want to remove.

Confirm your action by clicking the **Revoke Access Token** button.
