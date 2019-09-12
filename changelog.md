# Changelog

## 0.3.2 - 2019-09-12

### Added

* You can now create alerts that are triggered when an event/log happens inside a transaction

### Fixed

* Added empty state when there are now events/logs in a transaction
* Fixed issue where loading two public contracts that have the same address on different networks would display only the first contract that was loaded
* Loader would spin indefinitely for alert history for the demo project

## 0.3.1 - 2019-09-11

### Added

* You can now view events/logs that were emitted inside a transaction. Navigate to the "Events / Logs" tab inside the transaction page.

## 0.3.0 - 2019-09-10

### Added

* Release our [official App](https://tenderlydev.slack.com/apps/AMP2VCNCX-tenderly) on the Slack directory
* Destination tab on the "Alerting" page inside a project
* Ability to connect your Slack channel and receive alerts on Slack

### Fixed

* Alert history now displays the correct timestamp when an alert was matched
* Scrolling inside the debugger will not scroll the entire page any more

{% page-ref page="integrations/slack.md" %}

## 



