# 👁️ Moderation Queue

The moderation queue provides staff commands for reviewing entries that have been submitted to it.

{% hint style="info" %}
The current built-in chat filters and AI path do not automatically put messages into this queue. Enabling the queue does not hold all chat for approval. For normal filter behavior, see the [Moderation Overview](overview.md); for background analysis, see the [AI Filter](ai-filter.md).
{% endhint %}

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/modqueue` | `/mq`, `/modq` | List pending entries | `lpcpro.modqueue` |
| `/modqueue view <id>` | — | View an entry | `lpcpro.modqueue` |
| `/modqueue approve <id>` | — | Approve an entry | `lpcpro.modqueue` |
| `/modqueue deny <id>` | — | Deny an entry | `lpcpro.modqueue` |
| `/modqueue denywarn <id>` | — | Deny and warn the sender | `lpcpro.modqueue` |
| `/modqueue clear` | — | Clear pending entries | `lpcpro.modqueue` + `lpcpro.modqueue.admin` |
| `/modqueue toggle` | — | Toggle admission to the queue | `lpcpro.modqueue` + `lpcpro.modqueue.admin` |

These are in-game staff commands. Entry details include the captured sender, channel, reason, age, and text, with clickable review actions.

## Lifetime

Entries are held in memory. The default timeout is five minutes, with expired entries cleaned up once per minute. Entries are not a durable chat archive and are cleared when the manager shuts down. Approval does not guarantee delivery if the sender is no longer online.

## Permissions

| Permission | Description |
|---|---|
| `lpcpro.modqueue` | View and manage queue entries |
| `lpcpro.modqueue.notify` | Receive notifications when an entry is submitted |
| `lpcpro.modqueue.admin` | Clear the queue or toggle admission; also needs the base command permission |
