# 👁️ Moderation Queue

The moderation queue lets staff review flagged messages before they appear in chat. Messages caught by filters or the AI filter can be held for manual approval.

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/modqueue` | `/mq`, `/modq` | List pending messages | `lpcpro.modqueue` |
| `/modqueue view <id>` | — | View message details | `lpcpro.modqueue` |
| `/modqueue approve <id>` | — | Approve and send to chat | `lpcpro.modqueue` |
| `/modqueue deny <id>` | — | Deny without warning | `lpcpro.modqueue` |
| `/modqueue denywarn <id>` | — | Deny and warn the player | `lpcpro.modqueue` |
| `/modqueue clear` | — | Clear all pending messages | `lpcpro.modqueue` |
| `/modqueue toggle` | — | Toggle the queue on/off | `lpcpro.modqueue` |

## How It Works

1. A message triggers a filter (swear filter, AI filter, etc.)
2. Instead of being cancelled or censored, it enters the moderation queue
3. Staff with `lpcpro.modqueue.notify` receive a notification
4. Staff review the message and choose to approve, deny, or deny with warning
5. Approved messages are sent to chat; denied messages are discarded

## Features

- Clickable action buttons in chat for quick review
- Automatic player warnings on deny
- Message timeout/expiration for unreviewed messages
- Queue notification system for online staff

## Permissions

| Permission | Description |
|---|---|
| `lpcpro.modqueue` | View and manage the moderation queue |
| `lpcpro.modqueue.notify` | Receive notifications when messages are queued |
