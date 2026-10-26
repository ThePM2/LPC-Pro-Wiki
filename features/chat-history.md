# 🔍 Chat History & Search

LPC Pro logs chat messages and provides commands for staff to view history and search logs.

## Commands

### Chat History

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/chathistory <player> [count]` | `/chatlogs`, `/clogs` | View a player's chat history | `lpcpro.chatlog.view` |
| `/chathistory channel <id> [count]` | — | View channel message history | `lpcpro.chatlog.view` |
| `/chathistory search <query>` | — | Search up to 50 matching entries | `lpcpro.chatlog.view` + `lpcpro.chatlog.search` |

### Chat Search

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/chatsearch <query>` | `/csearch`, `/searchchat`, `/findchat` | Search chat logs by content | `lpcpro.chatlog.search` |
| `/chatsearch player:<name> [query]` | — | Search by player (optional content filter) | `lpcpro.chatlog.search` |
| `/chatsearch channel:<id> [query]` | — | Search by channel | `lpcpro.chatlog.search` |
| `/chatsearch time:<duration> <query>` | — | Search content within a time range | `lpcpro.chatlog.search` |
| `/chatsearch channel:<id> time:<duration> limit:<count> [query]` | — | Combine filters and a result limit | `lpcpro.chatlog.search` |

### Time Duration Format

The `time:` filter accepts these formats:

| Format | Example | Description |
|---|---|---|
| `Xs` | `30s` | Last 30 seconds |
| `Xm` | `30m` | Last 30 minutes |
| `Xh` | `2h` | Last 2 hours |
| `Xd` | `7d` | Last 7 days |

### Examples

```
/chatsearch diamond
/chatsearch player:Steve
/chatsearch channel:global time:1h limit:50 grief
```

## Features

- Advanced multi-filter search
- Time-based filtering
- Clickable search results
- Message type labels (CHAT, PM, COMMAND) in stored results
- Bounded result counts: 20 by default, at most 100 for player/channel history or `limit:` search

`/chathistory` requires a player; `/chatsearch` also works from console. Search needs a content query, a known `player:` filter or a `channel:` filter: `time:` alone does not start a query. The command does not provide a `type:` filter or page navigation.

Logging is configured in `features/chat-logging.yml`; database storage must be healthy. New entries are written in batches, so a newly sent message may not appear instantly. These staff commands can expose recorded private messages; grant access only to trusted staff. Existing stored command records can also appear in results, but the current player-command path does not call the command logger.

## Configuration

The generated defaults are:

```yaml
enabled: true
private-messages: true
commands: false
retention-days: 30
```

`retention-days` is limited to 1–3,650 days. Run `/lpc reload` after editing this file. `/lpc status` shows pending and unsaved log counts if storage is falling behind.

The `commands` key is read and retained, but enabling it does not currently attach command recording to player commands. [Command spy](../commands-and-permissions.md#staff-utility-commands) is a separate feature and does not make those commands durable history entries.

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.chatlog.view` | `op` | View chat history |
| `lpcpro.chatlog.search` | `op` | Search chat logs |
