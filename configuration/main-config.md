# Main Configuration

The main configuration file is `config.yml`, located in `plugins/LPC-Pro/`. It controls global plugin settings and hook toggles.

## Default Configuration

```yaml
# Check for plugin updates on startup.
check-for-updates: true

# After editing these settings, the server must be restarted for the changes to take effect.
enable-private-messages: true
# If private messages are enabled, ignoring messages will also be enabled, even if it is set to false.
enable-ignore-messages: true

# Plugin integrations - enable/disable hooks for other plugins
hooks:
  # Enable ItemsAdder integration for custom emojis (:emoji:) and font images in chat
  items-adder: true
  # Enable PlaceholderAPI integration for %placeholder% support
  placeholder-api: true
  # Enable Oraxen integration for custom glyphs (:glyph:) in chat
  oraxen: true
  # Enable ViaVersion integration for client version detection
  via-version: true
  # Enable Geyser/Floodgate integration for Bedrock player detection
  geyser: true
  # Enable ProtocolLib integration for message interception and deletion
  protocol-lib: true
  # Enable vanish integration (SuperVanish, PremiumVanish, Essentials)
  vanish: true
```

## Settings Reference

### General

| Key | Type | Default | Description |
|---|---|---|---|
| `check-for-updates` | boolean | `true` | Check for new plugin versions on startup |
| `enable-private-messages` | boolean | `true` | Enable `/msg` and `/reply` commands |
| `enable-ignore-messages` | boolean | `true` | Enable `/ignore` command (auto-enabled when PMs are on) |

### Hooks

All hooks are under the `hooks:` section. Only enable hooks for plugins you have installed.

| Key | Plugin | Description |
|---|---|---|
| `items-adder` | ItemsAdder | Custom emoji replacement (`:emoji:`) |
| `placeholder-api` | PlaceholderAPI | `%placeholder%` support in formats |
| `oraxen` | Oraxen | Custom glyph replacement (`:glyph:`) |
| `via-version` | ViaVersion | Client version detection |
| `geyser` | Geyser + Floodgate | Bedrock player detection |
| `protocol-lib` | ProtocolLib | Message deletion and interception |
| `vanish` | SuperVanish / PremiumVanish / Essentials | Hide vanished players from chat, mentions, PMs |

{% hint style="warning" %}
Changes to `enable-private-messages` and `enable-ignore-messages` require a **server restart** because commands are registered dynamically on startup.
{% endhint %}

## Reloading

Most configuration changes can be applied with `/lpc reload`. Exceptions:

- `enable-private-messages` / `enable-ignore-messages` — Require restart
- `database.yml` — Requires restart
