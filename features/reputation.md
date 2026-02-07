# Reputation

The reputation system lets players give karma points to other players, with leaderboards and cooldowns. Configuration is in `features/reputation.yml`.

## Commands

| Command | Description | Permission |
|---|---|---|
| `/rep <player>` | Give +1 reputation to a player | `lpcpro.rep.give` |
| `/rep view <player>` | View a player's reputation | `lpcpro.rep.view` |
| `/rep top` | View the reputation leaderboard | `lpcpro.rep.top` |

## Configuration

```yaml
enabled: true

reputation:
  cooldown-hours: 24       # Hours between giving rep to the same player
  points-per-rep: 1        # Points awarded per /rep command
  starting-reputation: 0   # Starting rep for new players
  allow-negative: false    # Allow negative reputation
  min-reputation: -100     # Minimum rep (if negative allowed)
  max-reputation: 999999   # Maximum rep cap

restrictions:
  no-self-rep: true              # Cannot rep yourself
  min-playtime-hours: 1          # Minimum hours played before giving rep
  min-playtime-receive: 0        # Minimum hours played before receiving rep

leaderboard:
  display-count: 10        # Players shown on leaderboard
  cache-seconds: 60        # Cache refresh interval

notifications:
  notify-recipient: true   # Notify player when they receive rep
  sound: "ENTITY_PLAYER_LEVELUP"
  sound-volume: 0.5
  sound-pitch: 1.5
```

## Settings Reference

| Setting | Type | Default | Description |
|---|---|---|---|
| `cooldown-hours` | integer | `24` | Cooldown before repping the same player again |
| `points-per-rep` | integer | `1` | Points given per `/rep` command |
| `no-self-rep` | boolean | `true` | Prevent players from repping themselves |
| `min-playtime-hours` | integer | `1` | Minimum playtime before a player can give rep |
| `allow-negative` | boolean | `false` | Allow reputation to go below zero |

## Placeholders

| Placeholder | Description |
|---|---|
| `%lpcpro_reputation%` | Player's current reputation score |
| `%lpcpro_reputation_rank%` | Player's rank on the leaderboard |

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.rep` | `true` | Base permission for rep commands |
| `lpcpro.rep.give` | `true` | Give reputation to others |
| `lpcpro.rep.view` | `true` | View reputation |
| `lpcpro.rep.top` | `true` | View leaderboard |
| `lpcpro.rep.bypass.cooldown` | `false` | Bypass rep cooldown |

## Achievements

Reputation milestones can unlock achievements (configured in `features/achievements.yml`):

- **Respected** — Reach 10 reputation
- **Beloved** — Reach 50 reputation
- **Community Idol** — Reach 100 reputation
