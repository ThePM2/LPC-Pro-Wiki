# 🆕 Newcomer System

The newcomer system provides special handling for new players, including a newcomer tag, welcome messages, slowmode restrictions, and mention limits. Configuration is in `features/newcomer.yml`.

## Configuration

```yaml
enabled: true

# Requirements to no longer be considered a newcomer
required-playtime-minutes: 60
required-message-count: 10

# Newcomer tag format (MiniMessage)
newcomer-tag: "<gray>[New]</gray>"

# Welcome message
show-welcome-message: true
welcome-messages:
  - "<green>Welcome to the server, <white>{player}<green>!"
  - "<gold>A new player has joined! Welcome, <white>{player}<gold>!"

# Restrictions
apply-slowmode: true
newcomer-slowmode-seconds: 5
mention-restriction: false
max-mentions-per-message: 1
```

## How It Works

A player is considered a "newcomer" until they meet **both** requirements:

1. Played for at least `required-playtime-minutes` minutes
2. Sent at least `required-message-count` messages

## Features

### Newcomer Tag

New players automatically receive the configured tag:

```yaml
newcomer-tag: "<gray>[New]</gray>"
```

This appears in chat via the `{tag}` placeholder until the player graduates from newcomer status.

### Welcome Messages

Random welcome messages are sent when a newcomer joins:

```yaml
welcome-messages:
  - "<green>Welcome to the server, <white>{player}<green>!"
  - "<gold>A new player has joined! Welcome, <white>{player}<gold>!"
```

### Slowmode

Newcomers can have an enforced slowmode, limiting how quickly they can send messages:

```yaml
apply-slowmode: true
newcomer-slowmode-seconds: 5  # 5 seconds between messages
```

### Mention Restrictions

Limit how many players newcomers can mention per message:

```yaml
mention-restriction: false     # Enable/disable
max-mentions-per-message: 1    # Max mentions when enabled
```

## Settings Reference

| Setting | Type | Default | Description |
|---|---|---|---|
| `required-playtime-minutes` | integer | `60` | Minutes of playtime to graduate |
| `required-message-count` | integer | `10` | Messages needed to graduate |
| `newcomer-tag` | string | `<gray>[New]</gray>` | Tag displayed for newcomers |
| `apply-slowmode` | boolean | `true` | Enforce slowmode on newcomers |
| `newcomer-slowmode-seconds` | integer | `5` | Seconds between messages |
| `mention-restriction` | boolean | `false` | Limit mentions for newcomers |
| `max-mentions-per-message` | integer | `1` | Max mentions when restricted |
