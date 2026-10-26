# ↪️ Public Chat Replies

Public replies let players respond to a recently delivered public message with a short quote of its original text. This is separate from `/reply` or `/r`, which remain private-message commands.

The feature is **disabled by default** and supports one chosen ordinary public channel on the current backend.

## Enabling Replies

Edit `plugins/LPC-Pro/chat/public-replies.yml`:

```yaml
enabled: true
channel: "global"
receipt-seconds: 120
max-excerpt-characters: 160
max-reply-characters: 256
```

The shipped defaults have `enabled: false`; the other values above are unchanged. Before enabling:

1. Choose a channel with `range: 0`, `permission: ""`, `auto-join: true`, `same-world: false` and `cross-server: false`.
2. Keep managed message deletion enabled in `advanced/message-deletion.yml` (`enabled: true`).
3. Keep the `chatreply` command enabled and grant `lpcpro.chat.reply.public` to participating players. The permission is allowed by default.
4. Use `/lpc reload`, then send a new message to that channel.

Replies are unavailable on Folia. Protected, local-range, same-world and cross-server channels are not eligible. Enabling replies does not change the channel's routing or grant access to it.

## Using a Reply

On Java, click the **Reply** action added to a newly delivered eligible message. It prepares the internal command with that message's token; type your reply after the prepared text and send it.

```text
/chatreply <delivered-token> That works for me
```

The token comes from the delivered action. It is not a player name, message number or token to copy from somebody else's chat. The command requires `lpcpro.chat.reply.public`.

Connected Bedrock players can select the message in `/chatmenu` and use **Public reply** when that action is available. See [Bedrock Support](../integrations/geyser.md).

A reply displays a plain quote above the new message, for example:

```text
↪ Steve: Meet at the village
Alex: That works for me
```

The new message uses normal channel formatting and moderation. The quote is inert: it does not re-run placeholders, mentions, inventory links or click actions from the original text.

## Audience & Expiry

A reply is available only while the original managed message is retained and the delivered action is valid for the recipient's current connection. The default action lifetime is 120 seconds. Author disconnects, recipient reconnects, reloads and original-message invalidation can make an action unavailable sooner.

Only players who received the original message and remain eligible for the reply audience can receive its contextual reply. Current channel access, ignore rules, visibility and personal receiving settings are checked again. A newly joined player does not gain the old context simply by joining the channel later.

Replies have **one level**. A contextual reply does not become a new source for another quoted reply chain. Quoted context is linked to managed deletion, so removing an original message also invalidates its related quote context rather than leaving an independently usable reference.

## Configuration Limits

| Setting | Default | Allowed values |
|---|---|---|
| `enabled` | `false` | `true` or `false` |
| `channel` | `"global"` | Exact eligible channel ID |
| `receipt-seconds` | `120` | `1`–`120` |
| `max-excerpt-characters` | `160` | `1`–`256` |
| `max-reply-characters` | `256` | `1`–`256` |

Receipts use a bounded temporary cache; they are not a permanent thread archive. If an action expires, send an ordinary new channel message instead.
