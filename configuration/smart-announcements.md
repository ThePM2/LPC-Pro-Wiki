# 📣 Smart Announcements

Smart announcements select eligible players using online count, total playtime, permissions, worlds, and server-local hours. Configuration is in `features/smart-announcements.yml`.

## Default Configuration

Fresh installations are silent:

```yaml
enabled: false
check-interval-seconds: 60
announcements: {}
```

## Defining Announcements

This is an optional example, not a shipped announcement. Merge it into the existing file:

```yaml
enabled: true
check-interval-seconds: 60
announcements:
  welcome_tip:
    enabled: true
    message: "<green>Welcome! <gray>Use <white>/toggle menu</white> to choose your chat settings."
    per-player: true
    cooldown-seconds: 300
    priority: 10
    random-chance: 1.0
    conditions:
      max_playtime_minutes: 30
    worlds: []
```

Run `/lpc reload` after editing.

### Announcement Properties

| Property | Default When Omitted | Description |
|---|---|---|
| `enabled` | `true` | Include this entry |
| `message` | Empty | MiniMessage text; supported placeholders resolve for the recipient |
| `per-player` | `false` | With `true`, send this entry at most once per player session |
| `cooldown-seconds` | `300` | Global interval before this entry can be considered again, including for per-player entries |
| `priority` | `5` | Higher values checked first |
| `random-chance` | `1.0` | Chance per eligible check, from 0 to 1 |
| `worlds` | Empty | Allowed world names; empty means all worlds |

At most one announcement entry is selected per check. Per-player entries are not recurring personal timers: after seeing the entry, that player is skipped until their session is reset by leaving/rejoining. A plugin restart also clears this in-memory history.

### Available Conditions

| Condition | Description |
|---|---|
| `min_players`, `max_players` | Inclusive online count bounds |
| `min_playtime_minutes`, `max_playtime_minutes` | Inclusive **total** playtime bounds from the player's Minecraft statistic |
| `permission` | Permission the recipient must have |
| `min_hour`, `max_hour` | Inclusive 0–23 hour bounds using the server machine's local clock |

Use the entry's `worlds` list for world filtering. `conditions.world` is not a supported runtime condition. Hour ranges do not wrap across midnight; use separate entries if needed.

## Examples

### Permission-Gated Announcement

```yaml
announcements:
  donor_tip:
    enabled: true
    message: "<gold>Thanks for supporting the server! <gray>Try your saved chat profiles."
    per-player: true
    cooldown-seconds: 300
    priority: 5
    random-chance: 1.0
    conditions:
      permission: "group.donor"
    worlds: []
```

### World-Specific Announcement

```yaml
announcements:
  pvp_tip:
    enabled: true
    message: "<red>PvP is enabled in this world."
    per-player: false
    cooldown-seconds: 600
    priority: 5
    random-chance: 1.0
    conditions:
      min_players: 2
    worlds:
      - "pvp_arena"
```

These are fragments for separate entries under your existing `announcements` map. Keep the top-level feature enabled. For simple timed broadcasts without conditions, use [Server Messages](server-messages.md).
