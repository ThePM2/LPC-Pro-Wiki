# Offline Messages

LPC Pro can queue private messages for offline players and deliver them when they next log in. Configuration is in `features/offlinemessages.yml`.

## How It Works

When a player sends a private message (`/msg`) to an offline player, the message is stored in the database. When the recipient logs in, all pending messages are delivered with a sound notification.

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
