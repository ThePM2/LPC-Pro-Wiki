# Smart Announcements

Smart announcements are context-aware messages that trigger based on conditions like player count, playtime, permissions, or world. Unlike regular timed announcements, they only send when their conditions are met. Configuration is in `features/smart-announcements.yml`.

## Configuration

```yaml
enabled: true

# How often to check conditions (seconds)
check-interval-seconds: 60
```

## Defining Announcements

Each announcement has a message, conditions, and delivery settings:

```yaml
announcements:
  welcome:
    enabled: true
    message: "<dark_gray>  »</dark_gray> <green>Welcome</green> <dark_gray>—</dark_gray> <gray>Welcome to the server!"
    per-player: true
    cooldown-seconds: 3600
    priority: 10
    random-chance: 1.0
    conditions:
      min_playtime_minutes: 0
      max_playtime_minutes: 5
    worlds: []
```

### Announcement Properties

| Property | Type | Description |
|---|---|---|
| `enabled` | boolean | Enable/disable this announcement |
| `message` | string | MiniMessage-formatted message text |
| `per-player` | boolean | `true` = per-player cooldown, `false` = global cooldown |
| `cooldown-seconds` | integer | Time before this announcement can trigger again |
| `priority` | integer | Higher priority announcements are checked first (1-10) |
| `random-chance` | float | Chance to send (0.0 to 1.0, where 1.0 = 100%) |
| `worlds` | list | Restrict to specific worlds (empty = all worlds) |

### Available Conditions

| Condition | Description |
|---|---|
| `min_players` | Minimum online player count |
| `max_players` | Maximum online player count |
| `min_playtime_minutes` | Player must have played at least X minutes this session |
| `max_playtime_minutes` | Player must have played at most X minutes this session |
| `permission` | Player must have this permission |
| `world` | Player must be in this world |

## Default Announcements

LPC Pro ships with these examples:

| Name | Trigger | Description |
|---|---|---|
| `welcome` | First 5 minutes of playtime | Welcome message for recent joins |
| `chat_tip` | After 30 minutes | Tip about @mentions |
| `busy_server` | 20+ players online | Acknowledgment of a busy server |
| `vote_reminder` | 5+ players, 30% chance | Vote reminder |
| `vip_tip` | Has `group.vip` permission, hub world | VIP-specific tip (disabled by default) |

## Examples

### Permission-Gated Announcement

```yaml
announcements:
  donor_perk:
    enabled: true
    message: "<gold>Thanks for donating! Use <white>/kit donor</white> for your daily rewards."
    per-player: true
    cooldown-seconds: 86400
    priority: 1
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
    message: "<red>PvP is enabled in this world! Watch your back."
    per-player: true
    cooldown-seconds: 600
    priority: 5
    random-chance: 1.0
    conditions: {}
    worlds:
      - "pvp_arena"
```
