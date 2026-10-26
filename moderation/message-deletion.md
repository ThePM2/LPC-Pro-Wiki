# 🗑️ Message Deletion

Staff can remove retained LPC Pro messages using the clickable delete button. LPC Pro can replay managed chat without the removed message; ProtocolLib adds capture of compatible outgoing messages and native signed deletion where available.

## Configuration

Settings are in `advanced/message-deletion.yml`:

```yaml
enabled: true
show-delete-button: true
delete-permission: "lpcpro.chat.delete"
message-retention-minutes: 10
notify-on-delete: false
notify-sender: true
```

This is an excerpt; keep the generated `delete-button-format` when editing other settings. It includes the message ID needed by the click action.

## Commands

| Command | Aliases | Description |
|---|---|---|
| `/deletemsg <messageId>` | `/delmsg`, `/removemsg` | Delete a retained message |
| `/clearchat [silent] [reason]` | `/cc`, `/chatclear` | Clear chat for eligible viewers |

Individual deletion is an in-game command and requires `lpcpro.chat.delete` plus the configured `delete-permission` if different. Clear chat requires `lpcpro.clearchat`; `lpcpro.clearchat.bypass` exempts a recipient from clearing. Message IDs are intentionally not offered in tab completion.

## Limits

Deletion works with the retained history, not every message a client has ever seen. ProtocolLib is optional for local managed replay and required for the additional packet interception path. Native signed deletion depends on server/client support and a captured signature; other cases use replay where possible. Messages from arbitrary plugins or modified client histories cannot be guaranteed to disappear.

Deleting a source invalidates its public reply receipts and matching reply-linked Bedrock menu entries. Existing inventory snapshot tokens have their own lifetime and are not revoked merely by deleting the chat message. AI Enforce mode can request deletion of a tracked matching message; successful automatic deletion logs the original message even when AI `log-analysis` is false. Individual deletion and packet interception are disabled on Folia.

See [ProtocolLib](../integrations/protocollib.md) for hook setup and [AI Filter](ai-filter.md) for post-hoc enforcement.
