# 🌐 Proxy / Network Support

LPC Pro can relay channel chat, private messages, player mutes, server mutes, and announcements between trusted BungeeCord or Velocity backends. Configuration is in `integration/proxy.yml` on each backend.

## Configuration

The integration is disabled by default. An enabled backend needs a unique name, its own secret, and at least one trusted peer:

```yaml
enabled: false
server-name: "survival"
authentication-secret: ""
trusted-server-secrets: {}
sync-channels: true
sync-private-messages: true
sync-mutes: true
sync-announcements: true
synced-channels: []
cross-server-format: "<gray>[{server}]</gray> {message}"
```

This example keeps the integration disabled until secrets are configured. Generate an independent random secret of at least 32 characters for each backend. Do not use a shared public/example password.

## Setup

1. Install the same signed-protocol LPC version on all participating backends.
2. Assign each one a unique `server-name` and its own `authentication-secret`.
3. Add each trusted peer's name and **that peer's secret** to `trusted-server-secrets`.
4. Enable the relevant sync options and set `enabled: true` after the trust configuration is ready.
5. For Velocity, set `bungee-plugin-message-channel = true` in `velocity.toml`. Configure plugin messaging and forwarding correctly for your proxy.
6. Protect backends from direct public connections, reject client-origin `lpcpro:main` forwarding at the proxy, and keep backend clocks synchronized.

For example, if survival uses secret A and hub uses secret B, survival trusts `hub: B`, while hub trusts `survival: A`. Replace A/B with the actual independently generated secrets; they are not literal configuration values.

{% hint style="warning" %}
Trust allows a peer to relay moderation actions as well as chat. Keep keys private. Old unsigned messages are rejected, so upgrade/configure trusted peers together. A shared SQL database does not replace proxy authentication.
{% endhint %}

## Sync Options

| Option | Default | Description |
|---|---|---|
| `sync-channels` | `true` | Relay eligible cross-server channels |
| `sync-private-messages` | `true` | Enable the cross-server PM relay |
| `sync-mutes` | `true` | Relay supported player/server mute changes |
| `sync-announcements` | `true` | Relay announcements |

These options only have an effect when the integration and trust configuration are valid. A shared database alone does not immediately invalidate every online cache on every backend.

## Channel Synchronization

Mark the channel `cross-server: true` in `chat/channels.yml`. An empty `synced-channels` list adds no further restriction; a nonempty list restricts forwarding to the listed IDs:

```yaml
synced-channels:
  - "global"
  - "staff"
```

The receiving backend must know and authorize the destination. Channel access and ignored/receiving settings still matter. An allowlist entry does not create a channel or make a private one public.

## Message Format

`cross-server-format` wraps the relayed text; a channel may override it with `cross-server-format` of its own.

| Placeholder | Description |
|---|---|
| `{server}` | Source backend name |
| `{prefix}` | Source prefix |
| `{player}` | Source player name |
| `{message}` | Relayed message text |
| `{channel}` | Channel name |

## How It Works

LPC Pro uses backend plugin messaging through the proxy. Signed packets include the origin, timestamp, and a replay-resistant nonce. Packets outside the 60-second clock window, unknown origins, old unsigned packets, and replayed messages are rejected. This is not an offline durable message broker: plugin messaging needs a carrier connection.

Use `/lpc reload` after editing the integration and inspect the server log before enabling production relay.
