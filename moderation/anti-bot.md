# 🕵️ Anti-Bot

The anti-bot system protects against chat bots and spam accounts by enforcing cooldowns after joining and detecting bot-like behavior. Configuration is in `moderation/antibot.yml`.

## Configuration

```yaml
enabled: true

# Seconds after join before player can chat
chat-cooldown-seconds: 5

# Seconds after join before player can use commands
command-cooldown-seconds: 3

# Maximum messages per minute (0 = unlimited)
max-messages-per-minute: 20

# Maximum similar messages before action
max-similar-messages: 3

# Similarity threshold (0.0 - 1.0)
similarity-threshold: 0.8

# Kick on detection (after 3 warnings)
kick-on-detection: true

# Kick message
kick-message: "Bot-like behavior detected."
```

## How It Works

### Join Cooldowns

New players must wait before interacting with chat:

- `chat-cooldown-seconds` — Wait before sending chat messages
- `command-cooldown-seconds` — Wait before using commands

### Rate Limiting

Players are limited to `max-messages-per-minute` messages per minute. Exceeding this rate triggers bot detection.

### Similarity Detection

If a player sends `max-similar-messages` messages that are more than `similarity-threshold` similar to each other, they are flagged.

### Kick on Detection

When `kick-on-detection` is `true`, players flagged for bot-like behavior are kicked after 3 warnings.

## Settings Reference

| Setting | Type | Default | Description |
|---|---|---|---|
| `chat-cooldown-seconds` | integer | `5` | Seconds after join before chatting |
| `command-cooldown-seconds` | integer | `3` | Seconds after join before commands |
| `max-messages-per-minute` | integer | `20` | Message rate limit (`0` = unlimited) |
| `max-similar-messages` | integer | `3` | Similar messages before flagging |
| `similarity-threshold` | float | `0.8` | How similar messages must be (0.0-1.0) |
| `kick-on-detection` | boolean | `true` | Kick flagged players |
