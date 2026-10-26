# 🚫 Anti-Advertising

The anti-advertising filter blocks URLs, IP addresses, and domains from being posted in chat. Configuration is in `moderation/moderation.yml`.

## Configuration

```yaml
anti-advertising:
  enabled: true

  # Block URLs/links
  block-urls: true

  # Block IP addresses
  block-ips: true

  # Domains that won't be blocked
  allowed-domains:
    - "example.com"
    - "yourserver.com"

  # Actions when advertising is detected
  actions:
    - CANCEL
    - WARN

  # Bypass permission
  bypass-permission: "lpcpro.bypass.advertising"
```

## How It Works

The filter checks chat messages for:

- **URLs** — Matches common URL patterns (http://, https://, www.)
- **IP Addresses** — Matches IPv4 addresses (e.g., `192.168.1.1`)
- **Domains** — Detects domain-like patterns (e.g., `someserver.net`)

### Allowed Domains

Domains listed in `allowed-domains` are excluded from detection. Use this to whitelist your own server's website, Discord invite, or other trusted domains.

```yaml
allowed-domains:
  - "yourserver.com"
  - "discord.gg"
  - "youtube.com"
```

## Actions

| Action | Description |
|---|---|
| `CANCEL` | Block the message |
| `SILENT_CANCEL` | Show a local sender copy while hiding it from normal recipients |
| `WARN` | Send the player a warning |

## Bypass

**Permission:** `lpcpro.bypass.advertising` (default: `op`)

Allowed-domain examples are policy choices: allowing `discord.gg`, for example, allows that domain rather than only one server invite. Reload with `/lpc reload` and test both an allowed domain and an unrelated blocked domain. This normal/content filter is not applied to every private message.
