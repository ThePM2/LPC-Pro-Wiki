# Server Links

LPC Pro can add custom links to the ESC/Pause menu using Paper's ServerLinks API. This feature requires **Paper 1.21+**.

## How It Works

When a player opens the pause menu (ESC), custom links are displayed alongside the standard options. Players can click these links to open URLs in their browser.

## Configuration

Server links are configured in `integration/server-links.yml`:

```yaml
enabled: true
```

## Link Types

LPC Pro supports the following built-in link types from Paper's `ServerLinks.Type` enum:

| Type | Description |
|---|---|
| `REPORT_BUG` | Bug report link |
| `COMMUNITY_GUIDELINES` | Community rules link |
| `SUPPORT` | Support/help link |
| `STATUS` | Server status page |
| `FEEDBACK` | Feedback form |
| `NEWS` | News page |
| `ANNOUNCEMENTS` | Announcements page |

{% hint style="warning" %}
The `CUSTOM` type is not a valid built-in link type. Links configured with type `CUSTOM` will be silently ignored. To add links with custom labels, use one of the built-in types above.
{% endhint %}

## Per-Link Permissions

Each link can require a permission to be visible. This allows showing different links to different player groups (e.g., staff-only links for admin panels).

## Requirements

{% hint style="warning" %}
Server Links require **Paper 1.21+**. This feature uses reflection for compatibility and will not be available on Spigot or older Paper versions.
{% endhint %}
