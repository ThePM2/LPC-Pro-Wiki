# 📥 Offline Messages

LPC Pro can queue private messages for offline players and deliver them when they next log in. Configuration is in `features/offlinemessages.yml`.

## How It Works

When a player uses `/msg` for a known offline player, LPC Pro can store the message in the database. The sender sees a queued confirmation only after the quota-checked insert succeeds. The recipient gets pending messages after login, in bounded batches that continue through the backlog during that session.

## Configuration

```yaml
enabled: true

messages:
  max-per-sender-daily: 10    # Max offline messages per sender per day
  expiration-days: 7           # Messages expire after 7 days
  cleanup-delivered-days: 30   # Clean up delivered messages after 30 days

delivery:
  join-delay-ticks: 40         # Delay before delivery (40 ticks = 2 seconds)
  max-delivery-batch: 20       # Max messages delivered at once

notifications:
  delivery-sound: "ENTITY_EXPERIENCE_ORB_PICKUP"
  sound-volume: 1.0
  sound-pitch: 1.0

restrictions:
  allow-self-send: false       # Allow sending messages to yourself
```

## Key Settings

| Setting | Default | Description |
|---|---|---|
| `max-per-sender-daily` | `10` | Prevents spam — limits how many offline messages one player can send per day |
| `expiration-days` | `7` | Undelivered messages are deleted after this period |
| `join-delay-ticks` | `40` | Waits 2 seconds after login before delivering (avoids join spam) |
| `max-delivery-batch` | `20` | Limits messages shown at once to avoid flooding |


## Privacy and Delivery

The normal `/msg` permission and private-message feature must be available. The recipient must be a known player who has joined before. Ignore lists, private-message preferences and DND are checked when accepting a queued message and again before delivery. A recipient with PMs off or DND on keeps pending messages for a later session; unavailable policy data prevents delivery.

The daily quota is per sender across the queue, not a separate allowance for each recipient. Expired undelivered messages are not delivered. The batch size bounds each delivery step; it does not discard messages beyond the first batch.

Each delivered entry has a stable `[#id]` marker. Delivery is at least once: a crash or failed acknowledgement can cause the same entry to appear again, so this is not a guaranteed exactly-once inbox. The marker lets recipients identify a repeat. Use the separate [Mail System](mail-system.md) when players need an inbox with explicit read, reply and delete controls.

Run `/lpc reload` after changing `features/offlinemessages.yml`. Keep the database and the entire LPC Pro data folder in your backup when updating.
