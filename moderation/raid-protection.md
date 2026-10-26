# 🚨 Raid Protection

Raid protection automatically activates when an abnormal number of players join in a short time window, helping protect against bot raids and mass-join attacks. Configuration is in `moderation/raidprotection.yml`.

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/raidmode` | `/raid`, `/raidprotection` | Toggle raid mode | `lpcpro.raidmode` |
| `/raidmode on` | — | Enable raid mode | `lpcpro.raidmode` |
| `/raidmode off` | — | Disable raid mode | `lpcpro.raidmode` |
| `/raidmode status` | — | Show current status | `lpcpro.raidmode` |
| `/raidmode trust <player>` | — | Add player to trusted list | `lpcpro.raidmode` |
| `/raidmode untrust <player>` | — | Remove from trusted list | `lpcpro.raidmode` |
| `/raidmode trusted` | — | List trusted players | `lpcpro.raidmode` |

## How It Works

1. LPC Pro monitors the join rate and message patterns
2. When thresholds are exceeded, **raid mode** activates automatically
3. During raid mode, new players are restricted and slowmode is applied
4. Automatic activations expire after the configured duration; staff can also turn mode off
5. Staff can also toggle raid mode manually

## Configuration

```yaml
enabled: true

auto-detection:
  enabled: true
  join-threshold: 5           # Players joining within time window
  join-time-window: 30        # Time window (seconds)
  message-threshold: 20       # Messages from new accounts
  message-time-window: 10     # Time window for messages (seconds)
  similarity-threshold: 0.8   # Message similarity (0.0-1.0)
  similar-message-count: 3    # Similar messages from different players

# How long a player is considered "new" (seconds)
new-player-duration: 300

# How long raid mode lasts when auto-triggered (seconds)
raid-mode-duration: 300

# Slowmode delay during raid mode (seconds)
slowmode-delay: 5

# Messages allowed through the raid/chat-shutdown restriction
chat-shutdown:
  allowed-messages:
    - "welcome"
    - "welcome back"
    - "wb"

# Trusted players bypass raid mode restrictions (UUIDs)
trusted-players: []
```

## Auto-Detection Triggers

Raid mode activates automatically when any of these conditions are met:

| Trigger | Config Keys | Description |
|---|---|---|
| Rapid joins | `join-threshold` + `join-time-window` | Too many players joining in a short window |
| Message flood | `message-threshold` + `message-time-window` | High message volume from new accounts |
| Similar messages | `similarity-threshold` + `similar-message-count` | Multiple new players sending similar messages |

## During Raid Mode

- Players considered new by the raid manager can be temporarily blocked from chat.
- A separate raid slowmode delay is applied alongside any manual delay.
- Staff alerts and current trust/bypass checks apply.
- Disabling raid protection clears its own restrictions and delay while preserving manually set slowmode.

The raid manager tracks how recently the player joined its current session. This is separate from persistent newcomer graduation. Rejoining starts a new session for this tracking.

Allowed messages are exact text by default; a trailing `*` allows a prefix, for example `welcome *`. Other filters and access rules may still reject the message. `/lpc reload` reloads the raid policy.

## Permissions

| Permission | Description |
|---|---|
| `lpcpro.raidmode` | Toggle raid protection and manage trusted list |
| `lpcpro.raidmode.bypass` | Bypass raid mode restrictions |
| `lpcpro.staff.alert` | Receive raid alerts |
