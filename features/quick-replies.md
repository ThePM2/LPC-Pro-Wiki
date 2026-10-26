# 💨 Quick Replies

Quick replies let players save frequently used messages and send them with a short command. Configuration is in `features/quickreply.yml`.

## Commands

| Command | Description |
|---|---|
| `/qr list` | List your saved quick replies |
| `/qr add <name> <message>` | Save a new quick reply with a name |
| `/qr remove <name>` | Remove a quick reply by name |
| `/qr <name>` | Send a saved quick reply |

**Aliases:** `/quickreply`, `/quickreplies`

**Permission:** `lpcpro.quickreply` (grant it explicitly to your player group)

## Configuration

```yaml
enabled: true

permissions:
  base: "lpcpro.quickreply"
  extra: "lpcpro.quickreply.extra"  # Permission for extra slots

limits:
  default-max: 5          # Default saved replies per player
  extra-max: 15           # Max replies with extra permission
  max-message-length: 200 # Maximum characters per saved reply
```

## Example Usage

1. Save a reply: `/qr add gg Good game everyone!`
2. Save another: `/qr add lfg Looking for players to join my team`
3. Send it later: `/qr gg` — Sends "Good game everyone!" to chat
4. List all: `/qr list` — Shows your saved replies
5. Remove one: `/qr remove lfg` — Removes the "lfg" reply

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.quickreply` | — | Use quick reply commands |
| `lpcpro.quickreply.extra` | — | Access to extra reply slots (15 instead of 5) |


## Saved Replies and Limits

Replies are stored per player in the database and survive reconnects. Names are case-insensitive, at most 20 characters, and use letters, numbers, `_` or `-`. Command words such as `list`, `add` and `remove` are reserved.

The shipped limit is five replies, or 15 with `lpcpro.quickreply.extra`. An owned and usable shop perk can raise this capacity without granting a permission. It does not grant access to `/qr` itself. Existing manual extra-slot access is respected.

The command accepts up to 256 characters, and the manager stores at most `limits.max-message-length` (200 by default); longer accepted messages are truncated to that stored limit. Use messages within the configured limit to keep the full text.

Sending `/qr gg` submits the saved text through the player's normal chat path, using the active write channel and its usual mute/moderation checks. It is not a private-message reply shortcut. Quick replies have their own permission and limits; they are separate from session-only [Macros](macros.md).

Run `/lpc reload` after editing quick reply settings. The `permissions.base`/`permissions.extra` entries are retained in the file, but the current command and extra-slot check use the built-in `lpcpro.quickreply` and `lpcpro.quickreply.extra` nodes; command access can be customized through `advanced/command-settings.yml`.
