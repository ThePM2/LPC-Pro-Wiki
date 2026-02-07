# LuckPerms

LPC Pro integrates with [LuckPerms](https://luckperms.net/) for group detection, prefixes, and suffixes in chat formats.

## What It Enables

- **Group Detection** — Determine player groups for per-group chat settings
- **Prefixes/Suffixes** — Display rank prefixes and suffixes in chat formats
- **Permission Checks** — All LPC Pro permissions are compatible with LuckPerms

## Setup

1. Install LuckPerms on your server
2. LPC Pro automatically detects LuckPerms — no additional configuration needed
3. Set `detection-mode: "LUCKPERMS_GROUP"` in `advanced/groups.yml` for group-based settings

## Group Detection

In `advanced/groups.yml`, set the detection mode:

```yaml
detection-mode: "LUCKPERMS_GROUP"
```

Group names in `advanced/groups.yml` must **exactly match** your LuckPerms group names:

```yaml
groups:
  owner:       # Must match LuckPerms group "owner"
    priority: 1000
    # ...
  admin:       # Must match LuckPerms group "admin"
    priority: 800
    # ...
```

## Prefixes and Suffixes

Set prefixes in LuckPerms:

```bash
/lp group owner meta setprefix 100 "<red>[Owner]</red>"
/lp group admin meta setprefix 90 "<dark_red>[Admin]</dark_red>"
/lp group vip meta setprefix 50 "<gold>[VIP]</gold>"
```

Then use them in chat formats with the `{prefix}` and `{suffix}` placeholders:

```yaml
player:
  text: "{prefix} {name} {suffix}"
```

{% hint style="tip" %}
Set `chat-prefix: ""` (empty) in `advanced/groups.yml` for any group to use the LuckPerms prefix instead of a custom one.
{% endhint %}

## PlaceholderAPI

With both LuckPerms and PlaceholderAPI installed, you can use LuckPerms placeholders in chat formats:

| Placeholder | Description |
|---|---|
| `%luckperms_prefix%` | Player's prefix |
| `%luckperms_suffix%` | Player's suffix |
| `%luckperms_primary_group_name%` | Primary group name |
| `%luckperms_groups%` | All groups |
