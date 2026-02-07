# ✨ Nicknames

Players can set custom nicknames that display in chat, private messages, and hover tooltips instead of their real username.

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/nick <nickname>` | `/nickname`, `/setnick` | Set your nickname | `lpcpro.nick` |
| `/nick off` | — | Remove your nickname (also accepts `reset`, `clear`, `remove`) | `lpcpro.nick` |

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.nick` | `true` | Set your own nickname |
| `lpcpro.nick.color` | `op` | Use color codes in nicknames |
| `lpcpro.nick.others` | `op` | Set nicknames for other players (not yet implemented) |

## Format Integration

When a player has a nickname set, the `{name}`, `{player}`, and `{nickname}` placeholders in chat formats will display the nickname instead of the real username:

```yaml
player:
  text: "{prefix}{tag} {name}"  # Shows nickname if set
```

The `{displayname}` placeholder reflects the Bukkit display name (set by other plugins or the server), not the LPC Pro nickname. Use `{name}` or `{nickname}` to show the LPC Pro nickname.
