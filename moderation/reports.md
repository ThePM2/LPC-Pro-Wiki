# 🚩 Reports

Players can report others for inappropriate behavior. Reports are reviewed by staff through a management interface.

## Commands

| Command | Description | Permission |
|---|---|---|
| `/report <player> [reason]` | Report a player | `lpcpro.report` |
| `/reports` | View pending reports | `lpcpro.reports.view` |
| `/reports list [status]` | List reports by status (pending/resolved/dismissed) | `lpcpro.reports.view` |
| `/reports view <id>` | View report details | `lpcpro.reports.view` |
| `/reports resolve <id> [note]` | Mark a report as resolved | `lpcpro.reports.manage` |
| `/reports dismiss <id> [note]` | Dismiss a report | `lpcpro.reports.manage` |
| `/reports player <name>` | View reports against a player | `lpcpro.reports.view` |

## How It Works

1. A player sends `/report Steve Toxic behavior`
2. Staff with `lpcpro.reports.view` are notified
3. Staff review with `/reports`
4. Staff resolve or dismiss with `/reports resolve <id>` or `/reports dismiss <id>`

## Chat Integration

Reports can also be submitted by clicking on a message in chat. The default chat format includes a hover tooltip on messages:

```yaml
message:
  text: "&f{message}"
  hover: "&eClick to report {name}'s message!"
  suggest: "/report {name} "
```

This pre-fills the report command when a player clicks on any message, making reporting quick and intuitive.

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.report` | `true` | Submit reports |
| `lpcpro.reports.view` | `op` | View pending reports |
| `lpcpro.reports.manage` | `op` | Resolve and dismiss reports |
