# ✏️ Grammar Correction

LPC Pro can automatically apply basic grammar corrections to chat messages, such as capitalizing the first letter and adding a period at the end. This creates a cleaner chat experience without manual enforcement.

## Configuration

Grammar settings are managed in `chat/grammar.yml`:

```yaml
enabled: false

# Auto-capitalize the first letter of messages
auto-capitalize: true

# Auto-add period at end of messages
auto-period: true

# Minimum message length to add a period
# Short messages like "ok" won't get a period
min-length-for-period: 3
```

## Features

| Feature | Description |
|---|---|
| Auto-capitalize | Capitalizes the first letter of every chat message |
| Auto-period | Adds a period at the end of messages that don't end with punctuation |
| Minimum length | Only adds periods to messages longer than the threshold |

The grammar system handles MiniMessage tags and legacy color codes correctly — it won't capitalize inside formatting tags.

## Bypass Permission

| Permission | Default | Description |
|---|---|---|
| `lpcpro.bypass.grammar` | `op` | Bypass auto grammar corrections |

Players with the `lpcpro.bypass.grammar` permission skip grammar corrections.
