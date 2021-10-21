# Configuration

Actions are configured in `tenderly.yaml` file. If you initialized actions project using `tenderly actions init`, this file is already created.

```yaml
# We'll only focus on actions section of tenderly.yaml. 
actions:
  # This is project identifed. You can have multiple actions project
  # in same directory, just run tenderly actions init again and choose
  # a different project and different source directory.
  Tenderly/actions-example:
    # Runtime version. Currently, only v1 is supported and represents Node 14.
    runtime: v1
    # This is path to directory with implementation. You can change this, but 
    # you must rename directory as well. This path is relative to location of
    # tenderly.yaml file.
    sources: actions
    # Following is a list of actions for this project.
    # To add new action, just add an entry to specs map.
    specs:
      # This is action name. Action name must be unique in project.
      # If action with same name is created, it will override existing action.
      # If action is renamed, new action will be created.
      # If you want to delete action, you must do it through dashboard.
      blockHelloWorld:
        # Optional description. Visible in dashboard.
        description: This is just an example, but you can publish this action.
        # This is function locator.
        # First part of locator defines a file, relative
        # to configured sources directory, in this case actions/block.{ts|js}.
        # File location is a path, so if you have src/ directory inside actions
        # this might be src/block:blockHelloWorldFn
        # Second part of locator is function name. Function must be exported from
        # specified file.
        function: block:blockHelloWorldFn
        # This is trigger configuration. Triggers are coverd in next section.
        trigger:
          # Trigger must have a type, which is one of
          # {transaction, block, periodic, webhook}.
          type: block
          # In this case, trigger is not configured, just type is selected.
          # To configure, block trigger, we must add block section here. More
          # about configuring triggers in next section.

```



Next, we are going to describe how to configure trigger for your action.
