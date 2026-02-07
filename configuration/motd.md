# 👋 MOTD (Message of the Day)

The MOTD system shows a welcome message to players when they join the server. It supports different messages for first-time players, returning players, and specific permission groups. Configuration is in `features/motd.yml`.

## Configuration

```yaml
enabled: true

# Delay before showing MOTD (ticks, 20 = 1 second)
delay-ticks: 40

# Permission to receive MOTD
permission: "lpcpro.motd"
```

## Default MOTD

Shown to returning players who don't match any group:

```yaml
default:
  - ""
  - "<gradient:gold:yellow>━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</gradient>"
  - ""
  - "  <gold>Welcome back, <white>{player}<gold>!</gold>"
  - ""
  - "  <gray>Online players: <white>{online}/{max}</white>"
  - ""
  - "  <aqua>/help</aqua> <gray>- View commands"
  - "  <aqua>/rules</aqua> <gray>- View server rules"
  - "  <aqua>/discord</aqua> <gray>- Join our Discord"
  - ""
  - "<gradient:gold:yellow>━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━</gradient>"
  - ""
```

## First Join MOTD

Shown only on a player's very first join:

```yaml
first-join:
  enabled: true
  messages:
    - "<rainbow>Welcome to the server, {player}!</rainbow>"
    - "<gray>Take a moment to read our <aqua>/rules</aqua>"
```

## Group-Specific MOTDs

Show different MOTDs based on permission:

```yaml
groups:
  staff:
    permission: "lpcpro.motd.staff"
    messages:
      - "<red>Welcome back, Staff Member <white>{player}</white>!"
      - "<gray>Online players: <white>{online}/{max}</white>"

  vip:
    permission: "lpcpro.motd.vip"
    messages:
      - "<gold>Welcome back, VIP <white>{player}</white>!</gold>"
      - "<gray>Thanks for supporting the server!"
```

Groups are checked in order — the first matching group is used. If no group matches, the default MOTD is shown.

## Placeholders

| Placeholder | Description |
|---|---|
| `{player}` | Player name |
| `{displayname}` | Player display name |
| `{online}` | Online player count |
| `{max}` | Max player count |
| `{world}` | Player's world name |
