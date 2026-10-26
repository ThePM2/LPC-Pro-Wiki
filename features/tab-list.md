# 📋 Tab List

LPC Pro can customize the tab list (player list) header and footer with dynamic information, placeholders, and animations. Configuration is in `features/tablist.yml`.

## Configuration

```yaml
enabled: true
update-interval-ticks: 40  # Refresh rate (40 ticks = 2 seconds)

header:
  - ""
  - "<gradient:gold:yellow><bold>YOUR SERVER NAME</bold></gradient>"
  - "<gray>play.yourserver.com</gray>"
  - ""

footer:
  - ""
  - "<gray>Online <white>{online}</white>/<white>{max}</white></gray>  |  <gray>Ping <white>{ping}ms</white></gray>  |  <gray>TPS <white>{tps}</white></gray>"
  - "<gray>Rank <white>{rank}</white></gray>  |  <gray>World <white>{world}</white></gray>"
  - ""
```

## Placeholders

### Built-in

| Placeholder | Description |
|---|---|
| `{player}` | Player name |
| `{displayname}` | Player display name |
| `{online}` | Online player count |
| `{max}` | Max player slots |
| `{tps}` | Server TPS |
| `{ping}` | Player ping (ms) |
| `{world}` | Current world name |
| `{time}` | Server time (HH:mm) |
| `{rank}` | Primary group (LuckPerms/Vault) |

### PlaceholderAPI

All PlaceholderAPI placeholders are supported if the plugin is installed.

## Formatting

Header and footer lines support MiniMessage formatting:

```yaml
header:
  - "<gradient:gold:yellow><bold>My Server</bold></gradient>"
  - "<rainbow>Welcome!</rainbow>"
```

## Update Interval

The `update-interval-ticks` controls how often the tab list refreshes. Lower values update more frequently but use more resources.

| Value | Frequency |
|---|---|
| `20` | Every 1 second |
| `40` | Every 2 seconds (default) |
| `100` | Every 5 seconds |


## Animated Header and Footer

Use a list of line lists for animation frames. One frame advances on each update interval:

```yaml
header:
  - ["<gold>My Survival Server</gold>", "<gray>Welcome, {player}!</gray>"]
  - ["<yellow>My Survival Server</yellow>", "<gray>Enjoy your stay!</gray>"]
```

`header` and `footer` animate independently according to the number of frames in each list. A normal list of strings remains a static multiline header/footer.

Enable `enable-tab-list` in `config.yml` and `enabled` in `features/tablist.yml`. The main switch needs a restart; header, footer and interval edits can use `/lpc reload`. This feature updates the header/footer; it does not configure the player-name entries or teams of a separate TAB plugin. If another plugin also writes the header/footer, choose which one should manage it.
