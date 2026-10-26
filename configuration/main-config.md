# 📝 Main Configuration

`plugins/LPC-Pro/config.yml` controls global feature switches, hooks, command ownership, and display settings. Feature-specific files are organized in the folders described in [Installation](../getting-started/installation.md).

## Default Configuration

These main settings are generated from the current configuration class:

```yaml
check-for-updates: true
update-notify-console: true
update-notify-join: true
enable-private-messages: true
enable-ignore-messages: true
enable-tags: true
enable-auto-tag: true
enable-mentions: true
enable-reputation: true
enable-polls: true
enable-achievements: true
enable-chat-games: true
enable-motd: false
enable-tab-list: true
enable-chat-bubbles: true
enable-translation: true
enable-discord: true
enable-mail: true
enable-grammar: true
enable-name-color: true
use-group-formats: true
strip-unresolved-placeholders: false
strip-unauthorized-color-codes: true
folia:
  allow-unsafe-console-commands: false
hooks:
  items-adder: true
  placeholder-api: true
  oraxen: true
  nexo: true
  via-version: true
  geyser: true
  protocol-lib: true
  vanish: true
```

This is a settings excerpt, not a replacement for your complete generated file. Keep the other sections, including command ownership and `/lpc info` formatting.

## Settings Reference

| Setting | What It Controls |
|---|---|
| `check-for-updates` | Startup update check; console and join notifications have separate switches |
| `enable-private-messages` / `enable-ignore-messages` | PM/ignore features; PMs also need ignoring enabled internally |
| `enable-tags` | All manual and automatic chat tags |
| `enable-auto-tag` | Permission-selected automatic tags; disabling this leaves manual tags available |
| Other `enable...` settings | Whether the corresponding manager/commands are initialized; the feature's own file may also require `enabled: true` |
| `enable-name-color` | Access to changing name color; already saved name colors remain applied |
| `use-group-formats` | Use primary-group format files; reloadable independently of the top-level `enable...` settings |
| `strip-unresolved-placeholders` | Strip unresolved `%placeholder%` text rather than leaving it visible |
| `strip-unauthorized-color-codes` | Remove unauthorized message color codes; `false` leaves those codes as literal text |
| `folia.allow-unsafe-console-commands` | Opt-in dispatch of configured console/reward commands on Folia |

## Hooks

Hooks default to `true`, but the matching provider must actually be installed and available. Setting a hook to `true` does not install it.

| Key | Integration |
|---|---|
| `items-adder`, `oraxen`, `nexo` | The provider's custom font/glyph syntax |
| `placeholder-api` | External PlaceholderAPI expansions |
| `via-version` | Client version detection |
| `geyser` | Genuine Geyser/Floodgate Bedrock detection and supported forms |
| `protocol-lib` | Supported outgoing message interception |
| `vanish` | Supported vanish providers/metadata |

See the [integration guides](../integrations/placeholderapi.md) for provider requirements. Install or remove provider plugins with a server restart.

## Command Conflicts

LPC Pro claims selected contested command labels by default:

```yaml
override-conflicting-commands:
  enabled: true
  commands:
    - msg
    - m
    - tell
    - t
    - whisper
    - w
    - r
    - reply
    - mail
    - email
    - ignore
    - unignore
```

Set `enabled: false` to leave contested labels with the other plugin. Removing a label returns it on `/lpc reload`; a single `"*"` entry allows all labels registered by LPC Pro to be claimed. The other plugin's namespaced command remains available. See [Command Customization](command-customization.md) before renaming commands or changing their permissions.

## Info Command Layout

`info-command` is a list of MiniMessage lines. It supports `{version}`, `{server_version}`, `{java_version}`, `{db_type}`, `{db_status}`, `{features}`, `{hooks}`, `{online}`, and `{max_players}`. `info-feature-format.enabled/disabled` and `info-hook-format.active/inactive` control the inserted status lines.

## Reloading

`/lpc reload` applies supported file changes and reports failures. **All top-level `enable...` switches keep their running values until a full restart.** Database connection settings also require restart. Check `/lpc status` afterward; an initialized manager is not proof that its own service is enabled or healthy.
