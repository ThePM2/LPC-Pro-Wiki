# 👍 Reputation

The reputation system lets players give karma points to other players, with leaderboards and cooldowns. Configuration is in `features/reputation.yml`.

## Commands

| Command | Description | Permission |
|---|---|---|
| `/rep <player>` | Give configured reputation points (default +1) | `lpcpro.rep.give` |
| `/rep view [player]` | View your own or a known player's reputation | `lpcpro.rep.view` |
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
| `lpcpro.rep.bypass.cooldown` | — | Bypass rep cooldown |

## Achievements

Reputation milestones can unlock achievements (configured in `features/achievements.yml`):

- **Respected** — Reach 10 reputation
- **Beloved** — Reach 50 reputation
- **Community Idol** — Reach 100 reputation


## Giving Reputation

Both `enable-reputation` in `config.yml` and `enabled` in this file must be on. The aliases are `/reputation` and `/+rep`. Every subcommand needs the base `lpcpro.rep` node as well as its action permission. These action nodes and the cooldown bypass can be customized under `permissions:` in `features/reputation.yml`.

```text
/rep Steve
/rep view
/rep view Steve
/rep top
```

The target must be a known player who has joined before. By default you cannot give reputation to yourself, you need one hour of recorded playtime to give it, and you must wait 24 hours before giving it to the same player again. A different target has a separate cooldown. The command awards the configured `points-per-rep`; it is not a command for entering an arbitrary positive or negative amount.

Points and cooldown writes use database storage. A rejected or failed update does not get a successful reputation acknowledgement. Run `/lpc reload` after editing the feature file; changing `enable-reputation` requires a restart.
