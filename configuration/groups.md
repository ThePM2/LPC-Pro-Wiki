# 👥 Groups

`advanced/groups.yml` defines LPC Pro's group detection and optional chat-prefix override. Your permission plugin still grants permissions, and primary-group **format selection** is handled separately.

## Detection Modes

| Mode | Description |
|---|---|
| `LUCKPERMS_GROUP` | Match the LuckPerms primary group to a configured group |
| `VAULT_GROUP` | Match the primary group supplied by the Vault chat provider |
| `PERMISSION` | Use the first configured permission match, in descending priority |

The shipped file selects `LUCKPERMS_GROUP`. If a provider is unavailable or cannot produce a matching group, detection falls back to the configured permission rules and then the default group. Group-name matching is case-insensitive.

## Example Configuration

This example uses permission-based detection and an explicit VIP prefix:

```yaml
detection-mode: "PERMISSION"
default:
  chat-prefix: ""
groups:
  vip:
    priority: 250
    permission: "lpcpro.group.vip"
    chat-prefix: "<gold>[VIP]</gold> "
```

Grant the permission in LuckPerms:

```text
/lp group vip permission set lpcpro.group.vip true
```

A non-empty `chat-prefix` overrides the prefix used in normal formatting. Leave it empty to use rank metadata from LuckPerms/Vault instead. Apply supported file edits with `/lpc reload`.

## Using with LuckPerms Prefixes

You can keep `chat-prefix: ""` and manage prefixes in LuckPerms:

```text
/lp group owner meta setprefix 100 "<red>[Owner]</red> "
/lp group admin meta setprefix 90 "<dark_red>[Admin]</dark_red> "
/lp group vip meta setprefix 50 "<gold>[VIP]</gold> "
```

Use `{prefix}` in the selected format. For primary-group format files such as `formats/groups/vip.yml`, see [Chat Formats](chat-formats.md). Changing the detection mode here does not change the format resolver into a permission-based format selector.

## Legacy Group Settings

The generated file also contains fields such as `message-cooldown`, `command-cooldown`, `max-mentions`, `max-message-length`, `can-use-colors`, `can-use-formatting`, `can-use-gradients`, `max-quick-replies`, `max-mail`, and moderation/slowmode/mute bypass flags. They can be loaded and displayed by group tools, but **the current message and command paths do not enforce these fields as group policies**.

Use the controls that the feature actually checks:

- [Message formatting permissions](../features/chat-formatting.md) for colors and formatting.
- [Anti-spam](../moderation/anti-spam.md) and [slowmode](../moderation/slowmode.md) for message intervals.
- [Mentions](../features/mentions.md) and [newcomer settings](../moderation/newcomer-system.md) for mention restrictions.
- [Quick replies](../features/quick-replies.md), [mail](../features/mail-system.md), and [shop perks](../features/chat-shop.md) for their own limits.
- The relevant explicit bypass permission from [Commands & Permissions](../commands-and-permissions.md).

Setting `bypass-moderation: true` or `can-use-colors: true` here is not a substitute for granting those permissions. The legacy file-level `enabled` key is not read by the current group manager either.
