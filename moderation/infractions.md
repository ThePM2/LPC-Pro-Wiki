# 📈 Infractions

Infractions are internal moderation points from AI enforcement and repeated local swear-filter violations. They are separate from player [reputation](../features/reputation.md) and manual [warnings](warnings.md).

## Configuration

The `infractions` section is in `moderation/moderation.yml`:

```yaml
infractions:
  enabled: true
  default-expiry-days: 7
  points:
    ai-filter: 2
    swear-filter: 1
  thresholds:
    mute:
      enabled: true
      points: 5
      duration: "30m"
    kick:
      enabled: true
      points: 10
    ban:
      enabled: true
      points: 15
      duration: "7d"
```

## How It Works

| Source | Default Points | When it is added |
|---|---|---|
| `swear-filter` | 1 | Three tracked local swear violations within two minutes |
| `ai-filter` | 2 | A matching AI verdict in Enforce mode, outside the penalty cooldown |

Not every cancelled message creates an infraction. Spam, caps, advertising, and cloud-only censorship do not independently use these point sources. Observe mode never awards AI points.

When active points cross a threshold upward, the highest applicable enabled action runs: mute at five, kick at ten, or ban at fifteen by default. Kicks have no duration setting. `lpcpro.infractions.bypass` exempts an online player from these automatic threshold actions; it does not mean that no record can be stored.

## Commands

These in-game staff commands require `lpcpro.infractions`:

| Command | Description |
|---|---|
| `/infractions <player>` | View active records and points |
| `/infractions top` | List players with the most active points |
| `/infractions history <player>` | Include expired records |
| `/infractions remove <player> #<id>` | Remove one record by its displayed ID |
| `/infractions clear <player>` | Clear that player's records |

## Expiration and Storage

Records expire after `default-expiry-days`; `0` means no expiry. Expired records no longer count toward active points but can be reviewed in history. Records are stored in `data/infractions.json` and retained across quit/rejoin and normal server restarts. Back up this file along with the database and other plugin data.
