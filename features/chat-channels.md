# Chat Channels

LPC Pro supports multiple chat channels, allowing players to separate conversations by purpose (global, local, staff, trade, help) or create custom channels. Configuration is in `chat/channels.yml`.

## Global Settings

```yaml
settings:
  default-channel: "global"     # Channel new players join
  allow-multi-channel: true     # Be in multiple channels at once
  show-channel-prefix: true     # Show channel prefix in messages
  channel-switch-message: "<gray>You are now chatting in <{color}>{name}<gray>."
```

## Defining Channels

Each channel is defined under the `channels:` section:

```yaml
channels:
  global:
    display-name: "Global"
    color: "#FFFFFF"
    range: 0               # 0 = unlimited reach
    permission: ""          # Empty = no permission required
    auto-join: true         # Players join automatically
    quick-prefix: "!"       # Type "!hello" to send to this channel
    same-world: false       # Restrict to same world
    cross-server: false     # Send across proxy servers
    format: "chat.yml"      # Format file from formats/ folder
```

### Channel Properties

| Property | Type | Default | Description |
|---|---|---|---|
| `display-name` | string | — | Display name in chat and UI |
| `color` | hex color | — | Channel color for formatting |
| `range` | integer | `0` | Block range for messages (`0` = unlimited) |
| `permission` | string | `""` | Permission required to join (empty = open) |
| `auto-join` | boolean | `false` | Automatically join on server login |
| `quick-prefix` | string | — | Shortcut prefix (e.g., `!` sends to global) |
| `same-world` | boolean | `false` | Only send to players in the same world |
| `cross-server` | boolean | `false` | Broadcast across proxy-connected servers |
| `format` | string | `"chat.yml"` | Chat format file to use |

## Default Channels

LPC Pro ships with five pre-configured channels:

| Channel | Prefix | Range | Permission | Description |
|---|---|---|---|---|
| `global` | `!` | Unlimited | None | Server-wide chat |
| `local` | `.` | 100 blocks | None | Nearby players only |
| `staff` | `#` | Unlimited | `lpcpro.channel.staff` | Staff-only communication |
| `trade` | `$` | Unlimited | None | Trading channel |
| `help` | `?` | Unlimited | None | Questions and help |

## Player Commands

| Command | Description |
|---|---|
| `/channel join <name>` | Join a channel |
| `/channel leave <name>` | Leave a channel |
| `/channel switch <name>` | Switch active speaking channel |
| `/channel list` | List available channels |
| `/channel <name>` | Quick-switch to a channel |
| `/ch <name>` | Shorthand alias for `/channel` |
| `/chat <name>` | Shorthand alias for `/channel` |

### Quick Prefix Usage

Instead of switching channels, players can use the quick prefix to send a single message to a specific channel:

- `!Hello everyone` — Sends "Hello everyone" to the **global** channel
- `.Hey neighbors` — Sends "Hey neighbors" to the **local** channel
- `#Staff meeting now` — Sends "Staff meeting now" to the **staff** channel

## Permissions

| Permission | Description |
|---|---|
| `lpcpro.channel` | Use channel commands |
| `lpcpro.channel.join.<channel>` | Join a specific channel |
| `lpcpro.channel.autojoin.<channel>` | Auto-join on server login |
| `lpcpro.channel.speak.<channel>` | Speak in a channel (separate from join) |
| `lpcpro.spy.channel` | Spy on all channel messages |

## Custom Channels

Add your own channels by adding entries under `channels:`:

```yaml
channels:
  faction:
    display-name: "Faction"
    color: "#FF00FF"
    range: 0
    permission: "lpcpro.channel.faction"
    auto-join: false
    quick-prefix: "@"
    same-world: false
    cross-server: false
    format: "chat.yml"
```

Each custom channel can use its own [chat format](../configuration/chat-formats.md) by creating a new format file in `formats/` and referencing it.
