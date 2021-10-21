# Periodic

Periodic trigger means your action will be invoked on a fixed schedule.&#x20;

```yaml
# Runs every 5 min: 00:00, 00:05, 00:10...
trigger:
  type: periodic
  periodic:
    # Supported values for interval are 
    # {5m, 10m, 15m, 30m, 1h, 3h, 6h, 12h, 1d}
    interval: 5m

```

Supported values for interval scheduling are: `5m`, `10m`, `15m`, `30m`, `1h`, `3h`, `6h`, `12h`, `1d`.

You can also use CRON scheduling. If you haven't worked with CRON, see [https://crontab.guru/](https://crontab.guru).

```yaml
trigger:
  type: periodic
  periodic:
    # At minute 5 past every hour.
    cron: "5 */1 * * *" 
```
