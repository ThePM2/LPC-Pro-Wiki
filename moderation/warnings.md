# ⚠️ Warnings

Staff can issue formal warnings with points and review them later. Manual warnings are stored in the database and are separate from the automatic [infraction system](infractions.md).

## Commands

### Warn Command

| Command | Description | Permission |
|---|---|---|
| `/warn <player> [points] <reason>` | Issue a warning; points default to one | `lpcpro.warn` |

```text
/warn Steve Please keep chat respectful
/warn Steve 2 Repeated advertising
```

### Warnings Command

The `/warnings` command has the alias `/warns`:

| Command | Description | Additional Permission |
|---|---|---|
| `/warnings` | View your own warnings | — |
| `/warnings <player>` | View a player's warnings | — |
| `/warnings remove <player> #<n>` | Remove the displayed warning number | `lpcpro.warn.remove` |
| `/warnings clear <player>` | Clear a player's warnings | `lpcpro.warn.clear` |
| `/warnings top` | Show the warning leaderboard | — |

All `/warnings` actions require `lpcpro.warn.view`. They are in-game commands; `/warn` also accepts a console sender.

## Automatic Threshold Actions

The current manual-warning manager uses these built-in defaults:

| Active Warning Points | Action |
|---|---|
| 5 | Kick |
| 10 | Permanent ban |

These thresholds are separate from `infractions.thresholds` in `moderation/moderation.yml`. There is no documented YAML setting for customizing the manual-warning thresholds. `lpcpro.warn.bypass` protects an online target from the applicable warning/threshold handling.

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.warn` | `op` | Issue warnings |
| `lpcpro.warn.view` | `op` | View and manage warning lists |
| `lpcpro.warn.remove` | `op` | Remove individual warnings |
| `lpcpro.warn.clear` | `op` | Clear warnings |
| `lpcpro.warn.bypass` | `op` | Warning bypass for the applicable target checks |
