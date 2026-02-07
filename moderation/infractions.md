# 📈 Infractions

The infraction system is an internal point-based tracking system for moderation. When chat filters detect violations, infraction points are automatically assigned. Points accumulate and trigger actions at configurable thresholds. Configuration is in `moderation/moderation.yml`.

{% hint style="info" %}
This is a **staff-only internal system**, separate from the player-facing reputation system. Players cannot see their infraction points.
{% endhint %}

## Configuration

```yaml
infractions:
  enabled: true

  # Days until infractions expire (0 = never)
  default-expiry-days: 7

  # Points per infraction source
  points:
    ai-filter: 2
    swear-filter: 1

  # Automatic actions at point thresholds
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

1. A player triggers a chat filter (swear filter, AI filter, etc.)
2. Infraction points are added based on the `points:` configuration
3. If the player's total active points reach a threshold, an automatic action is triggered
4. Infractions expire after `default-expiry-days` days

## Point Sources

| Source | Default Points | Description |
|---|---|---|
| `swear-filter` | 1 | Triggered by the swear/profanity filter |
| `ai-filter` | 2 | Triggered by the AI content filter |

## Threshold Actions

| Action | Default Points | Description |
|---|---|---|
| Mute | 5 | Automatically mute the player |
| Kick | 10 | Kick the player from the server |
| Ban | 15 | Temporarily ban the player |

Each threshold action can be individually enabled/disabled and configured with a duration.

## Expiration

Infractions expire after `default-expiry-days` days. Set to `0` to make infractions permanent. This allows players to gradually recover from minor offenses.
