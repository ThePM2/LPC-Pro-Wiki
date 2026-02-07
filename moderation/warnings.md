# ⚠️ Warnings

The warning system lets staff issue formal warnings to players. Warnings accumulate and can trigger automatic actions (mute, kick, ban) at configurable thresholds.

## Commands

### Warn Command

| Command | Description | Permission |
|---|---|---|
| `/warn <player> [points] <reason>` | Issue a warning (points default to 1) | `lpcpro.warn` |

### Warnings Command

The `/warnings` command (alias: `/warns`) handles viewing and managing warnings:

| Command | Description | Permission |
|---|---|---|
| `/warnings` | View your own warnings | `lpcpro.warn.view` |
| `/warnings <player>` | View a player's warnings | `lpcpro.warn.view` |
| `/warnings remove <player> #<n>` | Remove a specific warning by number | `lpcpro.warn.remove` |
| `/warnings clear <player>` | Clear all warnings for a player | `lpcpro.warn.clear` |
| `/warnings top` | Show players with the most warnings | `lpcpro.warn.view` |

## Automatic Threshold Actions

When a player accumulates enough warnings, automatic actions can be triggered. These are configured alongside your warning policy.

Common threshold configuration:

| Warnings | Action |
|---|---|
| 3 | Temporary mute (30 minutes) |
| 5 | Kick |
| 7 | Temporary ban (1 day) |
| 10 | Permanent ban |

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.warn` | `op` | Issue warnings |
| `lpcpro.warn.view` | `op` | View another player's warnings |
| `lpcpro.warn.remove` | `op` | Remove individual warnings |
| `lpcpro.warn.clear` | `op` | Clear all warnings for a player |
| `lpcpro.warn.bypass` | `op` | Bypass warning threshold actions (kick/ban) |
