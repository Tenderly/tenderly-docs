---
description: Examples of how to spawn DevNets using Bash and JavaScript
---

# Automated DevNet Spawning: Bash & JavaScript

### Prerequisites

Before proceeding, ensure your system meets these requirements:

1. `bash` and/or `node` installed on your system.
2. [Tenderly CLI](https://github.com/Tenderly/tenderly-cli) installed and authenticated.

### Clone repository with scripts

Clone GitHub repository:

```bash
git clone git@github.com:Tenderly/devnet-examples.git
```

Navigate into the cloned repository:

```bash
cd devnet-examples/spawn-devnet-auto
```

You will find two directories with code for spawning DevNets: a bash (`spawn-devnet.sh`) and other JS directory (`spawn-devnet.js`).

### Bash Script Example

1.  Navigate to `bash` folders:

    ```bash
    cd ./bash
    ```
2.  Create a `.env` file in your project directory and include the necessary environment variables:

    ```bash
    TENDERLY_DEVNET_TEMPLATE=your_template
    TENDERLY_PROJECT_SLUG=your_project_slug
    ```
3.  To run the script, use the following command in your terminal:

    ```bash
    ./spawn-devnet.sh
    ```
4. The script spawns a DevNet, extracts the RPC URL, and sets it as an environment variable in your `.zshrc` file.

### JavaScript Script Example

1.  Navigate to the js directory

    ```bash
    cd ./js
    ```
2.  Create a `.env` in your project root, include the following values:

    ```bash
    TENDERLY_ACCESS_KEY=your_access_key
    TENDERLY_PROJECT_SLUG=your_project_slug
    TENDERLY_DEVNET_TEMPLATE=your_devnet_tempalte
    TENDERLY_ACCOUNT_ID=your_account_id
    ```
3.  To run the script, use the following command in your terminal:

    ```bash
    yarn spawn-devnet
    ```
4. The script spawns a DevNet, extracts the RPC URL, and updates it in your `.env` file.



Through the above steps, you can seamlessly spawn DevNets in your development workflow using either **Bash** or **JavaScript**.
