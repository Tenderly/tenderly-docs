# Exporting a Local Transaction

**Many of our users are using Tenderly Forks for workflows that require Local Transactions.** Unlike Forks, Local Transactions might have small differences in execution between local nodes and the production network. If you are considering using Local Transactions, we strongly encourage you to check out our [Fork Customization](../simulations-and-forks/reference/tenderly-fork-customization-via-api/) section and our [**Integration Guides**](../simulations-and-forks/integration-guides/) - **Forks also support JSON RPC so you can use them just like any other node!**&#x20;

{% hint style="success" %}
Please reach out via Intercom if you need any help or have some feature requests regarding switching your workflow to Forks.
{% endhint %}

{% hint style="info" %}
We will be showing the example of how to export a local transaction for the purposes of debugging on Tenderly via Tenderly CLI.
{% endhint %}

Whether you already have an existing project or you are creating a new one, you will be able to export local transactions to your Tenderly dashboard in order to debug them properly.

![](<../.gitbook/assets/Screenshot 2021-10-14 at 15.52.12.png>)

![](<../.gitbook/assets/Screenshot 2021-10-14 at 15.53.14.png>)

To fork a network locally you can use the `tenderly export init` command:

![](<../.gitbook/assets/Screenshot 2021-10-14 at 15.54.53.png>)

![](<../.gitbook/assets/Screenshot 2021-10-14 at 15.55.33.png>)

![](<../.gitbook/assets/Screenshot 2021-10-14 at 15.56.06.png>)

By using the `tenderly export [tx hash]` command you will get a unique URL which you can use to debug your local transaction on Tenderly:

![](<../.gitbook/assets/Screenshot 2021-10-14 at 15.57.28.png>)
