# 🔗 Server Links

LPC Pro can add links to a compatible Minecraft client's pause menu using the server's ServerLinks API. This needs a server exposing the 1.21+ API; both Paper and Spigot API paths are supported when the required methods are available.

## Configuration

Settings are in `integration/server-links.yml`:

```yaml
enabled: true
links:
  - type: "CUSTOM"
    label: "Our Website"
    url: "https://example.com"
  - type: "COMMUNITY_GUIDELINES"
    url: "https://example.com/rules"
  - type: "SUPPORT"
    url: "https://example.com/staff-help"
    permission: "lpcpro.staff"
```

Replace example URLs with your own. `CUSTOM` is supported and uses `label` as literal display text. Standard types use the client's translated label.

## Link Types

| Type | Description |
|---|---|
| `CUSTOM` | Your own label |
| `REPORT_BUG` | Bug report |
| `COMMUNITY_GUIDELINES` | Community rules |
| `SUPPORT` | Help/support |
| `STATUS` | Service status |
| `FEEDBACK` | Feedback |
| `NEWS` | News |
| `ANNOUNCEMENTS` | Announcements |

Available standard types depend on the server API. Unknown types or unavailable API methods do not add a link.

## Per-Link Permissions

Omit `permission` for a public link. Set a permission to show it only to eligible players when their links are applied. A hidden link is not an access-control system for the destination website itself.

## Reloading

`/lpc reload` reloads the configured links. They are applied when players join; reconnect to see the new list. Older clients, translated connections, and servers without the API may not display these menu entries.
