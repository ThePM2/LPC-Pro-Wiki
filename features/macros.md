# ⚡ Macros

Macros are pre-defined message templates that staff and players can send with a single command. LPC Pro supports both global macros (saved in `features/macros.yml`) and personal macros (per player, for the current login session).

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/macro <name>` | `/macros` | Send a macro message | `lpcpro.macro` |
| `/macro <name> <player>` | — | Send macro with `{player}` replacement | `lpcpro.macro` |
| `/macro list` | — | List all available macros | `lpcpro.macro` |
| `/macro set <name> <message>` | — | Create/update a global macro | `lpcpro.macro.admin` |
| `/macro remove <name>` | — | Delete a global macro | `lpcpro.macro.admin` |
| `/macro personal <name> <message>` | — | Create a personal macro for this session | `lpcpro.macro` |
| `/macro personal <name> -` | — | Remove your personal macro | `lpcpro.macro` |

## How It Works

Type `/macro rules` to send the predefined "rules" message. Use `/macro rules Steve` to substitute "Steve" for `{player}`; this argument does not make the message private. Macros broadcast to all online players with a `[Staff]` prefix, independently of the active channel, its audience and normal chat moderation. Give `lpcpro.macro` only to people who should have this broadcast access.

Personal macros take precedence over global macros with the same name. They are cleared on quit; use [Quick Replies](quick-replies.md) for saved personal messages that survive reconnecting and go through normal player chat. Macro text and placeholder output are displayed as literal text rather than granting MiniMessage actions.

### Variable Substitution

Macros support these variables:

| Variable | Description |
|---|---|
| `{player}` | Target player name (from command argument) |
| `{sender}` | Name of the player sending the macro |

## Default Macros

LPC Pro adds these built-in global macros when creating a missing `features/macros.yml` for the first time:

| Macro | Purpose |
|---|---|
| `rules` | Remind players to read the rules |
| `spam` | Warning for spamming |
| `language` | Warning for inappropriate language |
| `ads` | Warning for advertising |
| `respect` | Remind players to be respectful |
| `help` | Direct players to help resources |
| `report` | Explain how to report players |
| `appeal` | Explain ban appeal process |
| `discord` | Share Discord invite link |
| `welcome` | Welcome message for new players |

## Permissions

| Permission | Description |
|---|---|
| `lpcpro.macro` | Use macros and create personal macros |
| `lpcpro.macro.admin` | Create, update, and remove global macros |


## Configuration

Global macros use this structure in `features/macros.yml`:

```yaml
global:
  event:
    message: "{sender}: Meet {player} at spawn for the building event."
    description: "Building event reminder"
```

Run `/lpc reload` after editing the file. `/macro set event Meet at spawn!` saves a global entry from in-game; it needs both `lpcpro.macro` and `lpcpro.macro.admin`. PlaceholderAPI, when installed, resolves against the sender. Replace the shipped example Discord link before using `/macro discord` on your server.

`/macro set` and `/macro remove` confirm success after the changed global list has been saved. Removed entries stay removed after reloads and restarts, including shipped default macros. An existing empty file or `global: {}` does not recreate the defaults.

For example:

```text
/macro set event Meet at spawn!
/macro remove event
/lpc reload
/macro list
```

The removed `event` entry remains absent. Global names are case-insensitive; removing a name also removes any differently capitalized copies of that name from the file. Existing spelling and additional fields on retained entries are preserved. If a file contains duplicate names that differ only by case, the last entry in file order is the active one.

If saving fails, the command reports an error and keeps the previous running macros. A failed configuration reload also keeps the last working list. Check storage access and the server log before retrying.
