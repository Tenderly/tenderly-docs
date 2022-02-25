# Pending vs Historical Block

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.43.31.png>)

If you choose to **simulate on a pending block**, by submitting your simulation Tenderly will slot it into the next available block to be mined with the appropriate transaction index within the block (i.e. next one at the moment of running the simulation).

![](<../../.gitbook/assets/Screenshot 2022-02-25 at 10.42.50.png>)

If you choose to **simulate on a historical block**, you can choose literally any block number - going back to the beginning of time i.e. the network you are simulating on - and any transaction index within that block to be executed by the simulation.

{% hint style="info" %}
By choosing the historical block and slotting your transaction with a custom index, Tenderly will technically eject one transaction from that block since the block size cannot be changed - this doesn't have any significant impact on the outcome of simulating a transaction within one block.



Features which would allow you to simulate the effect propagation from the historical block onwards might be coming in the future.
{% endhint %}

