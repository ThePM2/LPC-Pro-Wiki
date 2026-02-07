# 🌐 Proxy / Network Support

LPC Pro supports cross-server communication for BungeeCord and Velocity networks. When enabled, chat messages, private messages, mutes, and announcements can be synchronized across all servers. Configuration is in `integration/proxy.yml`.

## Configuration

```yaml
enabled: false

# Unique name for this server
server-name: "server"

# Sync options
sync-channels: true
sync-private-messages: true
sync-mutes: true
sync-announcements: true

# Channels to sync (empty = use cross-server flag in channels.yml)
synced-channels: []

# Cross-server message format
cross-server-format: "<gray>[{server}]</gray> {message}"
```

## Setup

1. Set `enabled: true` in `integration/proxy.yml` on each server
2. Give each server a unique `server-name` (e.g., "survival", "skyblock", "hub")
3. Ensure your BungeeCord/Velocity proxy has plugin messaging enabled

## Sync Options

| Option | Default | Description |
|---|---|---|
| `sync-channels` | `true` | Broadcast channel messages across servers |
| `sync-private-messages` | `true` | Allow `/msg` between players on different servers |
| `sync-mutes` | `true` | If muted on one server, muted everywhere |
| `sync-announcements` | `true` | Send announcements to all servers |

## Channel Synchronization

By default, channels marked as `cross-server: true` in `chat/channels.yml` are synced. You can override this with the `synced-channels` list:

```yaml
synced-channels:
  - "global"
  - "staff"
```

## Message Format

The `cross-server-format` wraps messages from other servers:

```yaml
cross-server-format: "<gray>[{server}]</gray> {message}"
```

| Placeholder | Description |
|---|---|
| `{server}` | Source server name |
| `{player}` | Player who sent the message |
| `{message}` | The formatted message |
| `{channel}` | Channel name |

## How It Works

LPC Pro uses Bukkit's plugin messaging channel system to communicate through the proxy. Messages are serialized and sent via the proxy to all connected servers running LPC Pro.
