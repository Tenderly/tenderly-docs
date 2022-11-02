# Commenting & Prioritizing Traces

Collaboration can be complex and time-consuming when you go through various contracts and Execution Traces ([**Function Trace and Call Trace**](execution-overview.md)). That is why you can comment on any trace, as well as set priorities.

When you click on any trace, you will have the comment bar on the bottom of the trace window, which you can open and again collapse on a click, regardless if you are posting the first comment or not. The number of comments on each trace are clearly displayed so you can easily see where the discussions are happening.

![](<../../.gitbook/assets/Screenshot 2022-01-17 at 15.14.56.png>)

When you select a trace, you can clearly prioritize it (and elaborate on it in the comments). In the top right of the trace window you can see the option _**Set priority**_ right next to [_View in Debugger_](../../debugger/how-to-use-tenderly-debugger/) button - clicking on it opens a dropdown from which you can select the priority you want for that particular trace and it will stay marked for all users that have access to the project until manually changed. Selecting _None_ for the priority of a trace removes the markings.

Lastly, clicking on the three dots next to _Set priority_ opens up a dropdown where you can [view the contract source](../../simulations-and-forks/how-to-simulate-a-transaction/editing-contract-source.md).

![](<../../.gitbook/assets/Screenshot 2022-01-17 at 15.16.29.png>)

When you collapse traces, only the parent trace will show the number of comments it has, and a new button (_Go to..._) will appear marking if child-traces have comments as well. Clicking on _Go to..._ will open a dropdown menu of all child-traces with comments so you easily jump to the commented trace. This also works in the same way for navigating to the child-traces with set priorities.

![](<../../.gitbook/assets/Screenshot 2022-01-17 at 15.18.47.png>)

All the comment and priority features persist through both Transaction Overview and Debugger views in your dashboard.

![](<../../.gitbook/assets/Screenshot 2022-01-17 at 15.21.04.png>)

You can pin any comment thread while you go through other traces. It will be unpinned when you click on another comment thread. You can also delete your comments.

![](<../../.gitbook/assets/Screenshot 2022-01-19 at 09.08.04.png>)
