# Changelog

## 1.3.5 - 2019-09-18

### Added

* We now support multiple revisions of a contract that was added to the dashboard via the [`tenderly push`](cli/commands/push.md) command

### Changed

* Contracts are now sorted by network in the project contracts page

### Fixed

* Error is now displayed when logging in via Google fails
* Loader for single alert page will not longer spin indefinitely if the alert does not exist

## 1.3.4 - 2019-09-17

### Added

* You can now view **state changes** in the execution tab in every transaction that had state changes.

## 1.3.3 - 2019-09-12

### Added

* You can now view **local variables** and **state variables** in the transaction debugger
* You can view event/log topics in the raw data section in a transaction

### Changed

* Events that were unable to be parsed no longer show raw data by default in the transaction events/logs tab

## 1.3.2 - 2019-09-12

### Added

* You can now create alerts that are triggered when an event/log happens inside a transaction

### Fixed

* Added empty state when there are no events/logs in a transaction
* Fixed issue where loading two public contracts that have the same address on different networks would display only the first contract that was loaded
* Loader would spin indefinitely for alert history for the demo project

## 1.3.1 - 2019-09-11

### Added

* You can now view events/logs that were emitted inside a transaction. Navigate to the "Events / Logs" tab inside the transaction page.

## 1.3.0 - 2019-09-10

### Added

* Release our [official App](https://tenderlydev.slack.com/apps/AMP2VCNCX-tenderly) on the Slack directory
* Destination tab on the "Alerting" page inside a project
* Ability to connect your Slack channel and receive alerts on Slack

### Fixed

* Alert history now displays the correct timestamp when an alert was matched
* Scrolling inside the debugger will not scroll the entire page any more

{% page-ref page="integrations/slack.md" %}

## 



