---
description: >-
  DevNets currently only support short-lived RPC URLs, which have a limited
  lifetime.
---

# RPC URL Lifetime

DevNets RPC URLs have a limited lifetime. This means that they will be available only for a certain period of time. Short-lived RPC URLs are typically used for testing and temporary integrations and are helpful when you want to restrict access for specific tasks or external collaborators.

The lifetime is measured from the first transaction that occurs on the RPC URL.

* **Idle Timeout (30 minutes):** The RPC URL has an idle timeout, which measures the amount of time that passes without any transactions occurring on the RPC URL, starting from the first transaction. If the idle timeout is reached, the RPC URL will become unavailable, and your DevNet run will be stopped.
* **Total Running Timeout (90 minutes):** The RPC URL also has a total running timeout, which measures the amount of time that passes from the first transaction on the RPC URL. If the total running timeout is reached, the RPC URL will become unavailable, and your DevNet run will be stopped.

If you experience issues with DevNet RPC URLs, please contact support at [support@tenderly.co](mailto:support@tenderly.co).

### **Creating a short-lived RPC URL via the Dashboard**

The fastest way to get to your short-lived RPC URL is via the Dashboard.

1. Navigate to the **DevNets** section from the lefthand menu in the Dashboard.
2. Click the button **Create a Template.**
3. Click on **Spawn DevNet.**
4. Click **Copy RPC Link.**

<figure><img src="../../.gitbook/assets/devnets copy url.png" alt=""><figcaption></figcaption></figure>

#### **Automated RPC URL creation**

To automate the creation of DevNet RPC URLs, you can use the Tenderly CLI.

Install and log into Tenderly

```bash
brew tap tenderly/tenderly && brew install tenderly
tenderly login
```

#### **Spawning an RPC URL**

```bash
tenderly devnet spawn-rpc --template <YOUR_TEMPLATE_SLUG> --project <YOUR_PROJECT_SLUG>
```

You can also use the `spawn-rpc` command with `access-key` or `token` flag to eliminate the need to run `tenderly login`

```bash
tenderly devnet spawn-rpc --template <YOUR_TEMPLATE_SLUG> --project <YOUR_PROJECT_SLUG> --account <YOUR_ACCOUNT_ID> --access-key <YOUR_ACCESS_KEY>
```

### Coming soon: Long-lived RPC URLs

We are currently developing a new feature with unlimited lifetimes, which will be available soon.&#x20;

In the meantime, you can use Tenderly Forks and please leave a feature request or submit any feedback or comments through the chat in the Dashboard or by sending an email to [support@tenderly.co](mailto:support@tenderly.co)

If you need to increase the lifetime, raise rate limits, or require any other modifications, please contact Support.
