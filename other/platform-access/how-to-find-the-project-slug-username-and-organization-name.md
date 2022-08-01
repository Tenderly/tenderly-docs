---
description: >-
  This guide shows you how to find the project name or slug, username, and
  organization name for use in various configuration files.
---

# How to Find the Project Slug, Username, and Organization Name

{% hint style="info" %}
Copy and paste the username, organization name, and project name or slug exactly as they appear. **Don’t make any changes**.
{% endhint %}

## Username

There are two ways to find your exact username: using the [**Tenderly Dashboard**](https://dashboard.tenderly.co/) and the [**Tenderly CLI**](https://github.com/Tenderly/tenderly-cli).

Open up your **Tenderly Dashboard:**

* Click on your profile picture in the top right nav bar.
* Under the [**Account**](https://dashboard.tenderly.co/account) section, go to **Settings**.
* The last field under **Profile Information** contains your username.

Using the **Tenderly CLI,** run the `tenderly whoami` command which will display your account `ID`, `email`, and `username`.

```bash
tenderly whoami
ID: 00000000-0000-0000-0000-000000000000
Email: demo@tenderly.co
Username: DemoUser
```

## Organization name

To get the organization name, you need to be part of an organization.

Open up your **Tenderly Dashboard:**

* Click on your profile picture in the top right nav bar.
* From the dropdown, click on [**Organizations**](https://dashboard.tenderly.co/organizations) to display a list of organizations you’re part of.
* Click on the name of your organization.
* In the left-hand sidebar, click on **Settings**.
* Under **General Settings,** the bottom field contains the organization name.

## Project name or slug

💡 Project name and project slug are used interchangeable and refer to the same thing.

Open up your **Tenderly Dashboard**:

* Locate the project picker in the top nav bar next to the Tenderly logo.
* From the dropdown, click on the name of the project to load it into the Dashboard.
* In the left-hand sidebar, click on **Settings**.

Alternative method:

* Click on your profile picture in the top right nav bar.
* From the dropdown, click on [**Projects**](https://dashboard.tenderly.co/projects) to display a list of your projects.
* Click on the name of the project to load it into the Dashboard or copy the project slug directly from the Slug column.
* In the left-hand sidebar, click on **Settings**.

Under the **Overview** section, you’ll see a URL for your project. This URL contains the project name/slug as well as your username or organization name.

`https://dashboard.tenderly.co/{ORGANIZATION_NAME}/**{PROJECT_SLUG}**`

To obtain the project name for a personal project, follow the same steps listed above. The only difference is that the `ORGANIZATION_NAME` portion of the URL will contain your username instead.

`https://dashboard.tenderly.co/{USERNAME}/**{PROJECT_SLUG}**`
