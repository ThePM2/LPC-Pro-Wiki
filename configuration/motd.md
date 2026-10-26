# 👋 MOTD (Message of the Day)

The MOTD is an **in-game welcome message** shown after joining, not the multiplayer server-list description. Configure it in `features/motd.yml`.

## Configuration

First set `enable-motd: true` in `config.yml` and restart. In `features/motd.yml`, enable the welcome message as well:

```yaml
enabled: true
delay-ticks: 20
show-player-head: false
permission: ""
default:
  - "<gold>Welcome back, <white>{player}</white>!"
  - "<gray>Online: <white>{online}/{max}</white>"
first-join:
  - "<green>Welcome to the server, <white>{player}</white>!"
groups:
  "lpcpro.motd.staff":
    - "<red>Welcome back, staff member <white>{player}</white>."
```

This is an opt-in example. Defaults are `enabled: false`, `delay-ticks: 20`, `show-player-head: true`, and `permission: ""`. The top-level `enable-motd` switch also defaults to `false`. A tick is 1/20 second at normal server speed.

An empty `permission` lets everyone receive the message. Set a node such as `lpcpro.motd` only if you want an explicit permission gate. `show-player-head` enables the optional head display; set it to `false` for simple full-width text.

## Default MOTD

The `default` list is used when no first-join or permission entry applies. Each list item is a formatted message line. Built-in placeholders and available PlaceholderAPI expansions are supported.

## First Join MOTD

`first-join` is a **list of lines**, not an `enabled/messages` section. A non-empty list takes precedence for a first-time player; an empty list leaves normal selection available.

```yaml
first-join:
  - "<rainbow>Welcome, {player}!</rainbow>"
  - "<gray>Enjoy your first visit."
```

## Group-Specific MOTDs

Keys under `groups` are permission nodes, and values are lists. Entries are checked in file order; the first permitted entry wins after the first-join check.

```yaml
groups:
  "lpcpro.motd.staff":
    - "<red>Welcome back, {player}!"
  "lpcpro.motd.vip":
    - "<gold>Thanks for supporting the server, {player}!"
```

The built-in `lpcpro.motd.vip` entry is deliberately skipped for operators so their general permission access does not automatically select that VIP greeting.

## Join Titles

An optional title is configured separately inside the same file:

```yaml
join-title:
  enabled: true
  delay-ticks: 60
  fade-in: 10
  stay: 60
  fade-out: 20
  default:
    title: "<gold>Welcome back!"
    subtitle: "<gray>Enjoy your stay, {player}"
  first-join:
    enabled: true
    title: "<green>Welcome to the server!"
    subtitle: "<gray>We're glad you're here, {player}"
  groups:
    "lpcpro.motd.staff":
      title: "<red>Welcome back, staff!"
      subtitle: "<gray>Hello, {player}"
```

Titles require the main `config.yml` `enable-motd` switch to be on. Within `features/motd.yml`, `join-title.enabled` controls titles independently of the welcome-text `enabled` setting. `join-title.enabled` defaults to `false`; its timing fields are ticks. Supported edits within this feature file can be reloaded with `/lpc reload`.

## Placeholders

| Placeholder | Description |
|---|---|
| `{player}` | Account name |
| `{displayname}` | Player display name |
| `{online}` | Online player count |
| `{max}` | Maximum player count |
| `{world}` | Player's current world |
