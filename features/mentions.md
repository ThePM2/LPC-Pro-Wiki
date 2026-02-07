# Mentions

Players can mention other players in chat using `@username` syntax, similar to Discord. Mentioned players receive a sound notification and see their name highlighted. Configuration is in `chat/mentions.yml`.

## Usage

| Syntax | Description | Permission |
|---|---|---|
| `@PlayerName` | Mention a specific player | `lpcpro.mention` |
| `@everyone` | Mention all online players | `lpcpro.mention.everyone` |
| `@here` | Mention players in the same world | `lpcpro.mention.everyone` |

## Configuration

```yaml
# Mention styling
color: "YELLOW"
bold: false
italic: false
underlined: true

# Sound notification
sound:
  enabled: true
  name: "entity.experience_orb.pickup"
  volume: 1.0
  pitch: 1.0

# Special mentions
everyone:
  enabled: true  # Requires lpcpro.mention.everyone

here:
  enabled: true  # Requires lpcpro.mention.everyone
```

## Styling

When a player is mentioned, their name is highlighted in chat according to the styling settings:

| Setting | Type | Default | Description |
|---|---|---|---|
| `color` | string | `YELLOW` | Highlight color for the mention |
| `bold` | boolean | `false` | Bold the mention text |
| `italic` | boolean | `false` | Italicize the mention text |
| `underlined` | boolean | `true` | Underline the mention text |

## Mention Limits

Per-group mention limits are configured in `advanced/groups.yml`:

```yaml
groups:
  member:
    max-mentions: 3      # Max @mentions per message
  vip:
    max-mentions: 5
  admin:
    max-mentions: -1     # Unlimited
```

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.mention` | `true` | Mention other players |
| `lpcpro.mention.receive` | `true` | Receive mention notifications |
| `lpcpro.mention.everyone` | `op` | Use `@everyone` and `@here` |

## Newcomer Restrictions

New players can have mention restrictions applied via `features/newcomer.yml`:

```yaml
mention-restriction: false
max-mentions-per-message: 1
```

When enabled, newcomers can only mention a limited number of players per message.
