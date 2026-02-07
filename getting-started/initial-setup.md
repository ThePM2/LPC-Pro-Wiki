# 🔧 Initial Setup

After [installing](installation.md) LPC Pro, follow this guide to get your server's chat configured.

## 1. Set Up Groups

If you use **LuckPerms** (recommended), open `advanced/groups.yml` and set:

```yaml
detection-mode: "LUCKPERMS_GROUP"
```

Make sure the group names in `advanced/groups.yml` match your LuckPerms group names exactly. For example, if you have a LuckPerms group called `admin`, there should be an `admin:` entry under `groups:`.

If you don't use LuckPerms, you can use permission-based detection:

```yaml
detection-mode: "PERMISSION"
```

With this mode, players need the `lpcpro.group.<name>` permission to be assigned to a group (e.g., `lpcpro.group.vip`).

## 2. Customize Chat Formats

Edit `formats/chat.yml` to change how chat messages appear. The format is split into **parts**, each with its own text, hover tooltip, and click action:

```yaml
player:
  text: "{prefix}{tag} {name}"
  hover:
    - "{prefix}{tag} {name}"
    - "&7Messages: &f%lpcpro_messages%"
    - ""
    - "&aClick to send a private message!"
  suggest: "/msg {name} "

divider:
  text: "&7➥"

message:
  text: "&f{message}"
```

See [Chat Formats](../configuration/chat-formats.md) for the full reference.

## 3. Configure Channels

Edit `chat/channels.yml` to define your chat channels. Each channel can have its own range, permission, format, and quick prefix:

```yaml
channels:
  global:
    display-name: "Global"
    color: "#FFFFFF"
    range: 0           # 0 = unlimited
    permission: ""     # empty = no permission required
    auto-join: true
    quick-prefix: "!"  # Type "!message" to send to this channel
    format: "chat.yml"

  local:
    display-name: "Local"
    color: "#AAAAAA"
    range: 100         # 100 blocks
    quick-prefix: "."
    same-world: true
```

See [Chat Channels](../features/chat-channels.md) for the full reference.

## 4. Configure Moderation

Edit `moderation/moderation.yml` to tune the chat filters. All filters are enabled by default with sensible defaults:

- **Anti-Spam**: 3-second message delay, 80% similarity threshold
- **Anti-Caps**: 70% caps threshold, auto-lowercase action
- **Anti-Advertising**: Blocks URLs and IPs
- **Swear Filter**: Censors profanity with automatic leet-speak detection

See [Moderation Overview](../moderation/overview.md) for details.

## 5. Enable Integrations

Edit `config.yml` to toggle plugin integrations:

```yaml
hooks:
  items-adder: true
  placeholder-api: true
  oraxen: true
  via-version: true
  geyser: true
  protocol-lib: true
  vanish: true
```

Only enable hooks for plugins you have installed.

## 6. Apply Changes

Run `/lpc reload` to apply your configuration changes.

## Next Steps

- [Configure your database](../configuration/database.md) if using MySQL
- [Set up Discord integration](../integrations/discord.md)
- [Review commands and permissions](../commands-and-permissions.md)
