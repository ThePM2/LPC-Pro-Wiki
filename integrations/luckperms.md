# 🍀 LuckPerms

LPC Pro uses LuckPerms for primary-group detection and rank metadata where available. LuckPerms can also manage all normal LPC permission nodes.

## Setup

1. Install LuckPerms.
2. Set `detection-mode: "LUCKPERMS_GROUP"` in `advanced/groups.yml` to use its primary group for LPC group settings.
3. Match LPC group IDs to the actual LuckPerms primary-group names.

```yaml
detection-mode: "LUCKPERMS_GROUP"
```

If LuckPerms is unavailable, this detection mode falls back to LPC permission-group selection and logs a warning.

## Group Settings and Formats

LPC groups in `advanced/groups.yml` control supported group settings. Per-group format files live in `formats/groups/`; `config.yml` must have `use-group-formats: true` for those files to participate in format selection.

```yaml
groups:
  admin:
    priority: 800
    chat-prefix: ""
```

This is an excerpt, not a replacement for the rest of the group's settings. An empty `chat-prefix` allows external rank metadata to be used; a nonempty LPC prefix overrides it. Use `/lpc diagnose <online-player>` to see the selected group and actual format origin.

## Prefixes and Suffixes

For example, set a LuckPerms prefix and use `{prefix}` in your format:

```text
/lp group vip meta setprefix 50 "<gold>[VIP]</gold> "
```

```yaml
player:
  text: "{prefix}{name}{suffix}"
```

Keep the other format parts. A player's selected color/tag and configured group formatting can affect the final result, so diagnose a real player rather than assuming group membership alone chooses a file.

## PlaceholderAPI

With the appropriate LuckPerms expansion installed, external `%luckperms_prefix%`, `%luckperms_suffix%`, and `%luckperms_primary_group_name%` values can also be used. See [PlaceholderAPI](placeholderapi.md).
