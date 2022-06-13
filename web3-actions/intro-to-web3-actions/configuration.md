# Configuration

Actions are configured in `tenderly.yaml` file. If you initialized the actions project using `tenderly actions init`, this file is already created.

```yaml
# We'll only focus on the actions section of tenderly.yaml. 
actions:
  # This is a project identifier. You can have multiple actions project
  # in the same directory, just run tenderly actions init again and choose
  # a different project and different source directory.
  tenderly/actions-example:
    # Runtime version. Currently, only v1 is supported and represents Node 14.
    runtime: v1
    # This is a path to the directory with implementation. You can change this, but 
    # you must rename the directory as well. This path is relative to the location of
    # tenderly.yaml file.
    sources: actions
    # Following is a list of actions for this project.
    # "specs" is a map from action name to action configuration.
    # To add a new action, just add an entry to the specs map.
    specs:
      # This is the action name. Action name must be unique in the project.
      # If an action with the same name is created, it will override the existing action.
      # If the action is renamed, a new action will be created.
      # If you want to delete the action, you must do it through the dashboard.
      blockHelloWorld:
        # Optional description. Visible in the dashboard.
        description: This is just an example, but you can publish this action.
        # This is a function locator.
        # First part of locator defines a file, relative
        # to configured sources directory, in this case actions/block.{ts|js}.
        # The file location is a path, so if you have src/ directory inside actions
        # this might be src/block:blockHelloWorldFn
        # Second part of the locator is the function name.
        # The function must be exported from specified file.
        function: block:blockHelloWorldFn
        # This is a trigger configuration. Triggers are covered in the next section.
        trigger:
          # Trigger must have a type, which is one of
          # {transaction, block, periodic, webhook}.
          type: block
          # In this case, a trigger is not configured, just a type is selected.
          # To configure a block trigger, we must add a block section here. More
          # about configuring triggers in the next section.  
      # An example of second action configuration in the same project.
      anotherBlockHelloWorld:
        # You can reuse same function in multiple actions.
        function: block:blockHelloWorldfn
        trigger:
          type: block
          # This is block trigger configuration. See Triggers section for
          # details on this and configuration of other trigger types.
          block:
            network: 1
            blocks: 100

```

{% hint style="success" %}
You can not specify multiple triggers for action. But you can reuse the function for multiple actions! Reusing function in actions with different trigger types is discouraged.
{% endhint %}



Next, we are going to describe how to configure a trigger for your action.
