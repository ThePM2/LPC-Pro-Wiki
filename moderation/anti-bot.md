# 🕵️ Anti-Bot

The anti-bot system protects against chat bots and spam accounts by enforcing cooldowns after joining and detecting bot-like behavior. Configuration is in `moderation/antibot.yml`.

## Configuration

```yaml
enabled: true

# Seconds after join before player can chat
chat-cooldown-seconds: 2

# Seconds after join before player can use commands
command-cooldown-seconds: 1

# Maximum tracked messages per minute (0 = unlimited rate)
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

Players without the bypass must wait after joining before interacting with chat:

- `chat-cooldown-seconds` — Wait before sending chat messages
- `command-cooldown-seconds` — Wait before using commands

### Rate Limiting

Players are limited to `max-messages-per-minute` messages per minute. Exceeding a positive limit triggers bot detection. Set it to `0` to disable only this rate limit; join cooldowns and similarity detection remain active. Unlimited rate mode does not collect a per-message rate history.

### Similarity Detection

If a new message matches at least `max-similar-messages` previous messages at or above `similarity-threshold`, the player is flagged. The comparison history retains up to five recent messages.

### Kick on Detection

When `kick-on-detection` is `true`, players flagged for bot-like behavior are kicked after 3 warnings.

## Settings Reference

| Setting | Type | Default | Description |
|---|---|---|---|
| `chat-cooldown-seconds` | integer | `2` | Seconds after join before chatting |
| `command-cooldown-seconds` | integer | `1` | Seconds after join before commands |
| `max-messages-per-minute` | integer | `20` | Message-rate limit; `0` disables this limit only |
| `max-similar-messages` | integer | `3` | Similar messages before flagging |
| `similarity-threshold` | float | `0.8` | How similar messages must be (0.0-1.0) |
| `kick-on-detection` | boolean | `true` | Kick after the detection warning threshold |

## Bypass and Scope

The values above match the current generator and bundled reference. Older files may have a five-second chat cooldown and three-second command cooldown; existing configured values are read as written. Keep your intended values when updating.

Negative `max-messages-per-minute` values are rejected with a warning while the previous valid rate is kept. On a first load, the fallback is `20`. The owner file is not rewritten to replace the invalid value. Set `enabled: false` to disable the whole anti-bot system.

`lpcpro.bypass.antibot` bypasses these checks. Grant it explicitly to intended staff in your permission plugin. Join cooldowns apply to this session and are separate from the persistent [newcomer policy](newcomer-system.md). This protects chat/command interactions after a player connects; it is not a network DDoS or proxy login filter.

Use `/lpc reload` after editing `moderation/antibot.yml`.
