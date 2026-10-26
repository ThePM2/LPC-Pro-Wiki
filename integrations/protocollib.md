# 📡 ProtocolLib

ProtocolLib adds packet interception to LPC Pro's retained chat system. It can capture compatible outgoing messages and send native signed-chat deletion packets when the server/client and captured signature support them.

## Setup

1. Install a ProtocolLib version compatible with your server.
2. Keep this setting in `config.yml`:

```yaml
hooks:
  protocol-lib: true
```

3. Restart after adding/removing the provider and check the startup log.

## Message Deletion

Staff with `lpcpro.chat.delete` can use a retained message's delete button or `/deletemsg <messageId>`. Local managed replay also works without ProtocolLib. ProtocolLib adds external packet capture and native signed deletion where available; it does not make every third-party message universally deletable.

See [Message Deletion](../moderation/message-deletion.md) for configuration, retention, permissions, and limitations. Client mods or retained copies cannot be forced to forget a message.

## Message Interception

`advanced/message-interceptor.yml` can match outgoing text and replace, modify, or block it. It defaults to enabled but needs a working ProtocolLib adapter. Rules support `name`, `match-type`, `pattern`, `action`, `replacement`, `case-sensitive`, and an optional `permission`.

```yaml
enabled: true
rules:
  - name: "server-prefix"
    match-type: "contains"
    pattern: "[OtherPlugin]"
    action: "replace"
    replacement: "[MyServer]"
    case-sensitive: false
```

This is a customization example. Review existing generated rules before replacing the list and test against the messages you intend to match.

{% hint style="info" %}
Packet interception and individual message deletion are disabled on Folia. Provider/server packet layouts also affect which messages can be intercepted.
{% endhint %}
