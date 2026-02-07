# Groups

Groups allow you to apply different chat settings per rank tier — different cooldowns, message lengths, color permissions, and moderation bypasses. Configuration is in `advanced/groups.yml`.

## Detection Modes

LPC Pro supports three ways to determine a player's group:

| Mode | Description |
|---|---|
| `LUCKPERMS_GROUP` | Uses the player's primary LuckPerms group (recommended) |
| `VAULT_GROUP` | Uses the player's primary Vault group |
| `PERMISSION` | Checks for `lpcpro.group.<name>` permissions |

```yaml
detection-mode: "LUCKPERMS_GROUP"
```

{% hint style="info" %}
When using `LUCKPERMS_GROUP`, the group names in `advanced/groups.yml` must **exactly match** your LuckPerms group names.
{% endhint %}

## Default Settings

Applied to players who don't match any group:

```yaml
default:
  message-cooldown: 3      # Seconds between messages
  command-cooldown: 1       # Seconds between commands
  max-mentions: 3           # Max @mentions per message
  max-message-length: 256   # Max characters per message
  can-use-colors: false     # Use & color codes in chat
  can-use-formatting: false # Use &l, &o, &n formatting
  can-use-gradients: false  # Use gradient formatting
  chat-prefix: ""           # Leave empty to use LuckPerms prefix
```

## Group Properties

Each group supports these settings:

| Property | Type | Description |
|---|---|---|
| `priority` | integer | Higher priority takes precedence (first match) |
| `permission` | string | Permission node for PERMISSION detection mode |
| `message-cooldown` | double | Seconds between messages (0 = no cooldown, supports decimals like `1.5`) |
| `command-cooldown` | double | Seconds between commands (0 = no cooldown, supports decimals like `0.5`) |
| `max-mentions` | integer | Max @mentions per message (-1 = unlimited) |
| `max-message-length` | integer | Max characters per message (-1 = unlimited) |
| `can-use-colors` | boolean | Allow `&` color codes in messages |
| `can-use-formatting` | boolean | Allow bold, italic, etc. |
| `can-use-gradients` | boolean | Allow gradient formatting |
| `bypass-moderation` | boolean | Skip all chat filters (not currently enforced — use individual bypass permissions) |
| `bypass-slowmode` | boolean | Ignore channel slowmode |
| `bypass-mute` | boolean | Chat even when server is muted (not currently enforced — use `lpcpro.bypass.mute` permission) |
| `chat-prefix` | string | Custom prefix (empty = use LuckPerms/Vault) |
| `max-quick-replies` | integer | Max saved quick replies for this group (default: 5) |
| `max-mail` | integer | Max mail messages in inbox for this group (default: 20) |

## Example Configuration

```yaml
groups:
  # Staff Groups
  owner:
    priority: 1000
    permission: "lpcpro.group.owner"
    message-cooldown: 0
    command-cooldown: 0
    max-mentions: -1
    max-message-length: -1
    can-use-colors: true
    can-use-formatting: true
    can-use-gradients: true
    bypass-moderation: true
    bypass-slowmode: true
    bypass-mute: true
    chat-prefix: ""

  admin:
    priority: 800
    permission: "lpcpro.group.admin"
    message-cooldown: 0
    max-mentions: -1
    max-message-length: 1000
    can-use-colors: true
    can-use-formatting: true
    can-use-gradients: true
    bypass-moderation: true

  mod:
    priority: 700
    permission: "lpcpro.group.mod"
    message-cooldown: 0
    max-mentions: 15
    max-message-length: 512
    can-use-colors: true
    can-use-formatting: true

  # Donator Groups
  mvp_plus:
    priority: 400
    permission: "lpcpro.group.mvpplus"
    message-cooldown: 0
    max-mentions: 10
    max-message-length: 500
    can-use-colors: true
    can-use-formatting: true
    can-use-gradients: true

  vip:
    priority: 250
    permission: "lpcpro.group.vip"
    message-cooldown: 2
    max-mentions: 5
    max-message-length: 350
    can-use-colors: true

  # Regular Players
  member:
    priority: 100
    permission: "lpcpro.group.member"
    message-cooldown: 3
    max-mentions: 3
    max-message-length: 256
    can-use-colors: false
```

## Using with LuckPerms Prefixes

Set `chat-prefix` to `""` (empty) for any group to use prefixes from LuckPerms instead:

```bash
/lp group owner meta setprefix 100 "<red>[Owner]</red>"
/lp group admin meta setprefix 90 "<dark_red>[Admin]</dark_red>"
/lp group vip meta setprefix 50 "<gold>[VIP]</gold>"
```

The `{prefix}` placeholder in your chat format will then display these LuckPerms prefixes automatically.
