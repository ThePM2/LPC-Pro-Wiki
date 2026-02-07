# Server Messages

Server messages control join, quit, death messages, automatic announcements, and chat clearing. Configuration is in `features/servermessages.yml`.

## Join Messages

```yaml
join:
  enabled: true
  public: true  # Show to all players
  format: "<green>+ <white>{player} <gray>has joined the server"
  first-join:
    enabled: true
    format: "<gold>Welcome <yellow>{player} <gold>to the server for the first time!"
```

| Setting | Description |
|---|---|
| `enabled` | Enable/disable join messages |
| `public` | If `true`, broadcast to all players. If `false`, show only to the joining player |
| `format` | MiniMessage-formatted message. `{player}` is replaced with the player's name |
| `first-join.enabled` | Show a special message for first-time players |
| `first-join.format` | First join message format |

## Quit Messages

```yaml
quit:
  enabled: true
  public: true
  format: "<red>- <white>{player} <gray>has left the server"
```

## Death Messages

```yaml
death:
  enabled: true
  public: true
  format: "<gray>{player} died"
  by-player-format: "<gray>{player} was killed by {killer}"
  by-mob-format: "<gray>{player} was killed by {mob}"
```

| Placeholder | Description |
|---|---|
| `{player}` | Name of the player who died |
| `{killer}` | Name of the killer (PvP) |
| `{mob}` | Name of the mob that killed the player |

## Automatic Announcements

Periodic announcements broadcast to the server:

```yaml
announcements:
  enabled: true
  interval: 600       # Seconds between announcements
  random: true         # Random selection vs. sequential order
  prefix: "<dark_gray>  » </dark_gray>"
  messages:
    - "<gold>Tip</gold> <dark_gray>—</dark_gray> <gray>Mention players with <yellow>@name</yellow>"
    - "<gold>Tip</gold> <dark_gray>—</dark_gray> <gray>Check your reputation with <yellow>/rep</yellow>"
    - "<gold>Tip</gold> <dark_gray>—</dark_gray> <gray>Customize your chat with <yellow>/tags</yellow>"
    - "<aqua>Info</aqua> <dark_gray>—</dark_gray> <gray>Need help? Use <yellow>/lpc help</yellow>"
```

## Clear Chat

Settings for the `/clearchat` command:

```yaml
clearchat:
  lines: 100  # Number of empty lines sent to clear the chat
  message: "<red><bold>CHAT CLEARED</bold></red><newline><gray>Cleared by <white>{player}</white></gray><newline><gray>Reason: <white>{reason}</white></gray>"
```

| Placeholder | Description |
|---|---|
| `{player}` | Staff member who cleared chat |
| `{reason}` | Reason provided (line is auto-removed if no reason given) |
