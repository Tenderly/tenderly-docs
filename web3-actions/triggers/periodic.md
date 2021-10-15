# Periodic

Periodic trigger means your action will be invoked on a fixed schedule. Here are a few examples:

```
# Runs every 5 min: 00:00, 00:05, 00:10, ...
trigger:
  type: periodic
  periodic:
	  interval: 5m # {"5m", "10m", "15m", "30m", "1h", "3h", "6h", "12h", "1d"}

# Or you can use cron
trigger:
  type: periodic
  periodic:
    cron: "*/5 * * * *"  # https://crontab.guru/
```
