# Quick Replies

Quick replies let players save frequently used messages and send them with a short command. Configuration is in `features/quickreply.yml`.

## Commands

| Command | Description |
|---|---|
| `/qr list` | List your saved quick replies |
| `/qr add <name> <message>` | Save a new quick reply with a name |
| `/qr remove <name>` | Remove a quick reply by name |
| `/qr <name>` | Send a saved quick reply |

**Permission:** `lpcpro.quickreply`

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
| `lpcpro.quickreply` | `true` | Use quick reply commands |
| `lpcpro.quickreply.extra` | `false` | Access to extra reply slots (15 instead of 5) |
