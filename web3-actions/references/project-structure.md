---
description: >-
  Learn about the structure of a Web3 Action project generated via CLI and
  understand the general layout of the tenderly.yaml configuration file.
---

# Project Structure

In this guide, you’ll learn how to navigate the files and project structure in a Web3 Action project generated via the Tenderly CLI.

Learn [how to use the Tenderly CLI](https://github.com/Tenderly/tenderly-cli).

## Project overview and root directory file structure

When you run the `tenderly actions init` command, the Tenderly CLI will create an _actions_ _root_ directory along with the necessary files. By default, the _actions root_ directory is named _actions_.&#x20;

However, you're able to specify another name during the initialization process. Once initialized, the name of the root directory can still be adjusted by changing the folder name and the `sources` field inside the `tenderly.yaml` file.

An **example** of a TypeScript-based Web3 Actions project structure:

```bash
src
|--- actions 			# actions root directory, can be renamed
|--- |--- example.ts
|--- |--- package.json
|--- |--- tsconfig.json
|--- |--- node_modules
|         |--- @tenderly-actions
|         |--- typescript
|--- tenderly.yaml
```

The _actions root_ directory contains the npm project for your Web3 Actions. All relevant files, including package.json, node\_modules, source files, and other dependencies, libraries, and resources, are contained in this folder.

**Default files include:**

* `actions/example.ts`: By default, this file contains all Web3 Actions.
* `tenderly.yaml`: This is a configuration file that specifies settings for all Web3 Actions in a project

{% hint style="warning" %}
The size of the zipped actions root directory, including `node_modules`, must be under 40MB. Make sure you stay below this limit when installing additional packages.
{% endhint %}

## The tenderly.yaml file structure

The `tenderly.yaml` file contains configurations and settings for a Tenderly project and all Web3 Actions.

For the purpose of this guide, the completed example `tenderly.yaml` file will look like this:

```yaml
account_id: "tenderly-username"
project_slug: "our-cool-project"
actions:
  our-org/our-cool-project:
    runtime: v2
    sources: actions
    specs:
      bestActionEver:
        description: Does the best thing ever
        function: very/organized/file:bestActionEver
        trigger:
          type: block
          block:
            network:
            - 3
            blocks: 10
```

Now, let’s break down what each section of this file does and how to configure it.

For easier understanding, think of the `tenderly.yaml` as containing two primary sections:

* **General configuration**: A section containing the name of the account and project the Web3 Action is associated with.
* **Web3 Actions configuration**: A section containing configurations for the Web3 Action itself, essentially informing Tenderly when it should be run.

### General configuration

The general configuration section includes the following key-value pairs:

```yaml
account_id: "johnDoe"
project_slug: "our-cool-project"
```

* `account_id`: Your username
* `project_slug`: Slug of the project associated with the Web3 Action (optional, can be left empty)

Check out this guide to learn how to [find the organization name, username, and project slug](../../other/platform-access/how-to-find-the-project-slug-username-and-organization-name.md).

### Web3 Actions configuration

The `actions` object is where you start defining your Web3 Actions, including the project settings, such as runtime, sources location, and the actual Web3 Action declaration.

```yaml
account_id: "johnDoe"
project_slug: ""
actions:
  my-username/my-cool-project:     # in case it's an individual project
# our-cool-org/our-cool-project:   # in case it's an org-level project
    runtime: v2
    sources: actions
    specs:
      ...
```

### Specifying the project

Start by specifying the composite key that uniquely identifies the project within the Tenderly platform.

* `username/project-slug`: Username and project slug for projects belonging to individual developers
* `org-name/project-slug`: Organization name and project slug if your project belongs to an organization

Check out this guide to learn how to [find the organization name, username, and project slug](../../other/platform-access/how-to-find-the-project-slug-username-and-organization-name.md).

{% hint style="info" %}
It's possible to use the same Web3 Actions project for multiple projects you have access to in the Tenderly Dashboard.
{% endhint %}

### Configuring the runtime

Next, you need to specify the runtime version and the directory that contains your Web3 Action code. This data is used by the Tenderly CLI to bundle and deploy your code to the Web3 Actions runtime on Tenderly’s infrastructure.

The following settings are mandatory:

* `runtime`: The runtime version. Currently, we support **v1**, which corresponds to Node 14 as the runtime environment and **v2**, which corresponds to Node 16.
* `sources`: The location of Web3 Action source files. The value must be a path pointing to the _actions root_ directory, relative to the folder containing the `tenderly.yaml` file. It should match the path you specified when running the init command.

**Example:** For the folder structure shown below, the proper value for **sources** would be `web3-actions`.

```bash
src
|-- web3-actions 			# actions root directory, can be renamed
|   |--- example.ts
|   |--- package.json
|   |--- tsconfig.json
|   |--- node_modules
|   	 |--- @tenderly
|        |--- /typescript
|-- tenderly.yaml
```

{% hint style="info" %}
If you change the `sources` value, a directory must exist at the specified path, relative to the _actions root_, and it must contain your source files with Web3 Action functions.
{% endhint %}

### Defining Web3 Actions settings

Individual Web3 Actions are declared under the `specs` object. You can declare multiple Web3 Actions in a single `tenderly.yaml` file.

Each Web3 Action must start with a key that represents the action name (`bestActionEver`). The action name must be unique at the project level. This key denotes how the deployed Web3 Action is named and represented in the Tenderly Dashboard.

The `description` key must also be included. The description is generally a sentence or two that describes what a Web3 Action does.

```yaml
specs:
  bestActionEver:
    description: Does the best thing ever!
```

Next, you need to specify the `function` key to link to the action function you want to run. Source code for Web3 Actions can be split among multiple files or nested in a custom directory structure. The `tenderly.yaml` file allows for seamless referencing.

For example, a function `bestActionEver` located in `actions/very/organized/file.ts` would be referenced in the yaml like so:

```yaml
our-org/our-cool-project:
  runtime: v2
  sources: actions
  specs:
    bestActionEver:
      description: Does the best thing ever
      function: very/organized/file:bestActionEver
      trigger:
        ...
```

The next step is to choose and define a trigger for the Web3 Action. A trigger is an event that Tenderly listens to and executes the Web3 Action once a criterion is met.

For an in-depth reference of triggers, explore [available Web3 Action Trigger Types](broken-reference).

When defining a **trigger** for a Web3 Action, the first thing to specify is its type. In the example below, we’re defining the _block_ trigger type. This means that the `bestActionEver` Web3 Action will run once every 10 blocks get mined on Rinkeby.

```yaml
bestActionEver:
  description: Does the best thing ever
  function: very/organized/file:bestActionEver
  trigger:
    type: block
    block:
      network:
      - 3
      blocks: 10
```

### Execution Types

Web3 Actions in Tenderly can be executed in two modes: **Sequential** and **Parallel**.

<figure><img src="../../.gitbook/assets/image (2) (4).png" alt=""><figcaption><p>Web3 Action Execution Type step in the Web3 Action UI Builder</p></figcaption></figure>

#### Sequential Execution

In sequential execution, actions are executed one by one in the order they were invoked. This is the default mode of execution. In this mode, each action waits for the previous action to complete before it begins execution. Here's an example of an action configuration for a sequential execution:

```diff
our-org/our-cool-project:
  runtime: v2
  sources: actions
  specs:
    bestActionEver:
      description: Does the best thing ever
+     execution_type: sequential
      function: very/organized/file:bestActionEver
      trigger:
        ...
```

#### Parallel Execution

In parallel execution, actions are executed in parallel, which leads to higher throughput. In this mode, the order of execution is not guaranteed and there may be possible race conditions with [action storage](https://docs.tenderly.co/web3-actions/references/context-storage-and-secrets#storage). Here's an example of an action configuration for a parallel execution:

```diff
our-org/our-cool-project:
  runtime: v2
  sources: actions
  specs:
    bestActionEver:
      description: Does the best thing ever
+     execution_type: parallel
      function: very/organized/file:bestActionEver
      trigger:
        ...
```
