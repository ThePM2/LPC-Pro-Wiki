# ✨ Nicknames

Players can set custom nicknames that display in chat, private messages, and hover tooltips instead of their real username.

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/nick` | `/nickname`, `/setnick` | Show your current nickname | `lpcpro.nick` |
| `/nick <nickname>` | — | Set your nickname | `lpcpro.nick` |
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


## Valid Names and Colors

A nickname's visible text must contain **3–16 letters, numbers or underscores**. It cannot include spaces, clickable actions, hover text, selectors or other dynamic components. The formatting input is limited to 512 characters. Players with `lpcpro.nick.color` can use colors, decorations, gradients and rainbow styling around an otherwise valid name.

```text
/nick Builder_One
/nick <aqua>Builder_One</aqua>
/nick reset
```

The colored example requires `lpcpro.nick.color`. Nicknames are saved in player settings and revalidated when rendered. The command changes your own nickname only; the declared `lpcpro.nick.others` node does not add an admin-target syntax.

Commands such as `/msg` still use real account names. `{name}` and `{player}` first use an LPC nickname; when one is absent, an external display name may be used before the real name. `%lpcpro_nickname_plain%` is useful for displaying the LPC nickname without styling. [Style Profiles](player-style-profiles.md) save name color, chat color and the selected tag; your current nickname stays separate.
