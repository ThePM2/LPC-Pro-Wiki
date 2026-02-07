# ⏱️ Anti-Spam

The anti-spam filter prevents message flooding by enforcing a cooldown between messages and detecting repeated/similar messages. Configuration is in `moderation/moderation.yml`.

## Configuration

```yaml
anti-spam:
  enabled: true

  # Minimum seconds between messages
  message-delay: 3

  # Similarity threshold (0-100)
  # Messages this similar to recent messages will be blocked
  similarity-threshold: 80

  # Number of recent messages to check for similarity
  similarity-check-count: 3

  # Actions when spam is detected
  actions:
    - CANCEL    # Cancel the message
    - WARN      # Warn the player

  # Bypass permission
  bypass-permission: "lpcpro.bypass.spam"
```

## How It Works

### Message Delay

When a player sends a message, they must wait `message-delay` seconds before sending another. If they try to send before the cooldown expires, the message is blocked.

### Similarity Detection

LPC Pro compares each new message against the player's last `similarity-check-count` messages. If any comparison exceeds the `similarity-threshold` percentage, the message is flagged as spam.

For example, with the default settings:
- "Can someone help me?" followed by "Can someone help me please?" (very similar) would be blocked
- "Hello" followed by "How is everyone?" (very different) would pass

## Actions

Available actions when spam is detected:

| Action | Description |
|---|---|
| `CANCEL` | Silently cancel the message (only sender sees it) |
| `WARN` | Send the player a warning message |

Multiple actions can be combined.

## Bypass

**Permission:** `lpcpro.bypass.spam` (default: `op`)

Players with this permission skip the spam filter.
