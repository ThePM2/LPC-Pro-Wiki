# 🔍 Chat History & Search

LPC Pro logs chat messages and provides commands for staff to view history and search logs.

## Commands

### Chat History

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/chathistory <player> [count]` | `/chatlogs`, `/clogs` | View a player's chat history | `lpcpro.chatlog.view` |
| `/chathistory channel <id> [count]` | — | View channel message history | `lpcpro.chatlog.view` |

### Chat Search

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/chatsearch <query>` | `/csearch`, `/searchchat`, `/findchat` | Search chat logs by content | `lpcpro.chatlog.search` |
| `/chatsearch player:<name> [query]` | — | Search by player (optional content filter) | `lpcpro.chatlog.search` |
| `/chatsearch channel:<id> [query]` | — | Search by channel | `lpcpro.chatlog.search` |
| `/chatsearch time:<duration> [query]` | — | Search within time range | `lpcpro.chatlog.search` |

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
/chatsearch diamond          # Find all messages containing "diamond"
/chatsearch player:Steve     # Find all messages from Steve
/chatsearch time:1h grief    # Find "grief" messages in the last hour
```

## Features

- Advanced multi-filter search
- Time-based filtering
- Clickable search results
- Message type filtering (CHAT, PM, COMMAND)
- Paginated results

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.chatlog.view` | `op` | View chat history |
| `lpcpro.chatlog.search` | `op` | Search chat logs |
