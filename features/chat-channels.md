# 📺 Chat Channels

LPC Pro supports multiple chat channels, allowing players to separate conversations by purpose (global, local, staff, trade, help) or create custom channels. Configuration is in `plugins/LPC-Pro/chat/channels.yml`.

## Global Settings

```yaml
settings:
  default-channel: "global"
  allow-multi-channel: true
  show-channel-prefix: true
  channel-switch-message: "<gray>You are now chatting in <{color}>{name}<gray>."
  auto-focus:
    enabled: false
    rules: []
```

Joining a channel lets a player receive its messages. The **active speaking channel** decides where ordinary messages go. A player can receive several channels while speaking in one.

## Defining Channels

Each channel is defined under the `channels:` section:

```yaml
channels:
  global:
    display-name: "Global"
    color: "#FFFFFF"
    range: 0
    permission: ""
    auto-join: true
    quick-prefix: "!"
    same-world: false
    cross-server: false
    format: "chat.yml"
```

### Channel Properties

| Property | Type | Default when omitted | Description |
|---|---|---|---|
| `display-name` | string | Channel ID | Display name |
| `color` | hex color | `"#FFFFFF"` | Channel color |
| `range` | integer | `0` | Block range (`0` = unlimited) |
| `permission` | string | `""` | Required access permission; empty means open |
| `auto-join` | boolean | `false` | Join automatically when access is allowed |
| `quick-prefix` | string | `""` | Send one message without switching |
| `same-world` | boolean | `false` | Restrict delivery to the sender's world |
| `cross-server` | boolean | `false` | Relay through the configured proxy integration |
| `cross-server-format` | string | Global proxy format | Optional format for incoming remote messages |
| `format` | string | `"chat.yml"` | File under `formats/` |

The shipped configuration supplies explicit values for each default channel. An available explicit channel format other than `chat.yml` wins; the `chat.yml` fallback marker allows a primary-group format to be selected first. See [Chat Formats](../configuration/chat-formats.md).

## Default Channels

| Channel | Quick prefix | Range | Access | Auto-join |
|---|---|---|---|---|
| `global` | `!` | Unlimited | Open | Yes |
| `local` | `.` | 100 blocks, same world | Open | No |
| `staff` | None | Unlimited | `lpcpro.channel.staff` | Yes, with access |
| `trade` | `$` | Unlimited | Open | No |
| `help` | `?` | Unlimited | Open | No |

The shipped staff channel has cross-server relay enabled. That still requires a working proxy setup. It has no `#` quick prefix by default; add `quick-prefix: "#"` to that channel if you want one.

## Player Commands

| Command | Description |
|---|---|
| `/channel` | Show help and automatic-focus status when enabled |
| `/channel join <name>` | Join a channel |
| `/channel leave <name>` | Leave a channel |
| `/channel switch <name>` | Select an already joined speaking channel manually |
| `/channel focus <name>` | Alias for `switch` |
| `/channel list` | List available channels |
| `/channel <name>` | Join if needed, then select manually |
| `/channel auto` | Follow automatic-focus rules again when enabled |
| `/ch <name>` | Alias for `/channel` |
| `/chat <name>` | Alias for `/channel` |

### Quick Prefix Usage

Players can send one message without changing their saved speaking choice:

- `!Hello everyone` — Send to **global**.
- `.Hey neighbors` — Send to **local**.
- `$Selling oak logs` — Send to **trade**.

Channel access and speaking restrictions still apply. Choose distinct prefixes and avoid conflicts with other chat features.

## Permissions

| Permission | Description |
|---|---|
| `lpcpro.channel` | Use `/channel`; allowed by default |
| The channel's configured `permission` | Access a protected channel, including receiving messages |
| `lpcpro.channel.deny.speak.<channel>` | Explicitly prevent speaking in that channel |
| `lpcpro.admin` | Bypass the explicit speaking-deny check |

Speaking is allowed after access checks unless a speaking-deny node is explicitly true. Operators also bypass that deny check. Protect staff and team conversations with the channel's `permission`; a name, quick prefix or automatic-focus rule does not provide access control.

## Custom Channels

Add entries under the existing `channels:` section:

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

Grant the configured access node to the intended players, then use `/channel faction`. Each custom channel can use its own [chat format](../configuration/chat-formats.md) by creating a file in `formats/` and referencing it.

## Automatic Channel Focus

Automatic focus is optional and disabled by default. It selects a speaking channel from the player's effective permissions, while manual switching remains available.

For example, first add a protected `red` channel under `channels:`:

```yaml
channels:
  red:
    display-name: "Red Team"
    color: "#FF5555"
    range: 0
    permission: "teams.red"
    auto-join: true
    quick-prefix: ""
    same-world: false
    cross-server: false
    format: "chat.yml"
```

Then merge this into the existing `settings:` section:

```yaml
settings:
  auto-focus:
    enabled: true
    rules:
      - permission: "teams.red"
        channel: "red"
        priority: 100
```

The highest-priority matching rule wins. Rules selecting the same channel can share a priority. If equally important rules select different channels, no rule matches, or the chosen channel is inaccessible, ordinary chat pauses with an explanation. It does not silently fall back to global.

Existing saved speaking choices remain **MANUAL** when automatic focus is enabled. Players opt in with `/channel auto`; `/channel switch <name>` returns to manual mode. Choices persist. A rule never grants channel access or bypasses a speaking deny.

After editing, use `/lpc reload` and check `/channel` as a member of each affected group. `/lpc diagnose <player> <channel>` helps explain the effective channel and format. On Folia, same-world and range-based channels remain unavailable in this version.

## Related Features

[Personal chat settings](chat-settings.md) can hide eligible public chat without leaving staff or local conversations. [Public replies](public-replies.md) add replies to one opted-in local public channel. Players can also share [inventory snapshots](inventory-sharing.md) and [coordinates](coordinates.md) in local channel messages.
