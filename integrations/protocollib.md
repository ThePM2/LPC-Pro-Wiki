# ProtocolLib

LPC Pro integrates with [ProtocolLib](https://www.spigotmc.org/resources/protocollib.1997/) for packet-level message manipulation, enabling features like message deletion and message interception.

## What It Enables

- **Message Deletion** — Staff can delete individual messages from all players' chat via a clickable `[X]` button
- **Message Interception** — Intercept and modify outgoing chat packets

## Setup

1. Install ProtocolLib on your server
2. Ensure `protocol-lib: true` is set in `config.yml` under `hooks:`

## Message Deletion

With ProtocolLib enabled, staff with the `lpcpro.chat.delete` permission can delete individual chat messages. When a message is deleted:

- It is removed from the chat window of **all** players who received it
- The deletion happens at the packet level, so the message disappears completely

### Permission

| Permission | Default | Description |
|---|---|---|
| `lpcpro.chat.delete` | `op` | Delete individual chat messages |

## How Message Deletion Works

LPC Pro uses ProtocolLib to track outgoing chat packets and their signatures. When a staff member triggers deletion, LPC Pro sends a packet to each player's client to remove the specific message from their chat window.

{% hint style="info" %}
Message deletion relies on the client respecting the deletion packet. Some modified clients may not honor the request.
{% endhint %}
