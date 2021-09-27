# Failed Transaction

Now that we have set up our new destinations let's see them in action!

For this example, we created an alert that will notify us whenever a transaction fails on the Dai Smart Contract. After setting up the alert we need to choose a destination:

![](../../.gitbook/assets/image%20%2848%29.png)

Here we’ll select our shiny new Sentry and PagerDuty destinations.

Now, whenever a Dai transaction fails, a man will come and tap you on the shoulder to inform you about it. Not really, but instead of that, you will have to settle for a detailed alert from Sentry and PagerDuty.

As you can see, the whole error stack-trace can be found on your Sentry dashboard:

![](../../.gitbook/assets/image%20%2835%29.png)

PagerDuty gives you a more straightforward insight into the issue:

![](../../.gitbook/assets/image%20%2841%29.png)

![](../../.gitbook/assets/image%20%288%29.png)

