# 🔠 Anti-Caps

The anti-caps filter prevents excessive use of capital letters in chat messages. Configuration is in `moderation/moderation.yml`.

## Configuration

```yaml
anti-caps:
  enabled: true

  # Minimum message length to check (short messages are ignored)
  minimum-length: 5

  # Maximum percentage of caps allowed (0-100)
  caps-threshold: 70

  # Action to take
  action: LOWERCASE   # CANCEL, WARN, or LOWERCASE

  # Bypass permission
  bypass-permission: "lpcpro.bypass.caps"
```

## How It Works

1. Messages shorter than `minimum-length` characters are ignored (e.g., "OK" or "GG" won't trigger the filter).
2. For longer messages, the filter calculates the percentage of uppercase letters.
3. If the percentage exceeds `caps-threshold`, the configured action is applied.

**Example** with default settings (70% threshold, 5 char minimum):
- `HELLO EVERYONE` — 100% caps, exceeds 70% → action taken
- `Hello everyone` — one uppercase letter, below 70% → allowed
- `HI` — Only 2 characters, below minimum length → ignored

## Actions

| Action | Description |
|---|---|
| `CANCEL` | Block the message entirely |
| `WARN` | Send a warning but allow the message |
| `LOWERCASE` | Lowercase excessive capitals while retaining sentence starts (default) |

## Bypass

**Permission:** `lpcpro.bypass.caps` (default: `op`)

The percentage uses letters rather than spaces or punctuation. Use `/lpc reload` after changing the settings.
