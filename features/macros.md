# ⚡ Macros

Macros are pre-defined message templates that staff and players can send with a single command. LPC Pro supports both global macros (shared by all staff) and personal macros (per player).

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/macro <name>` | `/macros` | Send a macro message | `lpcpro.macro` |
| `/macro <name> <player>` | — | Send macro with `{player}` replacement | `lpcpro.macro` |
| `/macro list` | — | List all available macros | `lpcpro.macro` |
| `/macro set <name> <message>` | — | Create/update a global macro | `lpcpro.macro.admin` |
| `/macro remove <name>` | — | Delete a global macro | `lpcpro.macro.admin` |
| `/macro personal <name> <message>` | — | Create a personal macro | `lpcpro.macro` |

## How It Works

Type `/macro rules` to instantly send the pre-defined "rules" message. Use `/macro rules Steve` to send it with `{player}` replaced by "Steve".

### Variable Substitution

Macros support these variables:

| Variable | Description |
|---|---|
| `{player}` | Target player name (from command argument) |
| `{sender}` | Name of the player sending the macro |

## Default Macros

LPC Pro ships with these built-in global macros:

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
