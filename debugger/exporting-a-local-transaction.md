# Exporting a Local Transaction

{% hint style="info" %}
We will be showing the example on how to export a local transaction for the purposes of debugging on Tenderly via Tenderly CLI.
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
