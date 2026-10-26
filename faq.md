# ❓ FAQ & Troubleshooting

## Frequently Asked Questions

### How do I reload the plugin?

Use `/lpc reload` with `lpcpro.admin`, then check `/lpc status`. Supported format and feature-file edits reload, but **all top-level `enable...` switches** in `config.yml` and database connection settings require a full server restart. Replace JARs with the server stopped. See [Updating & Recovery](getting-started/updating.md).

### Chat format changes aren't showing up

Run `/lpc diagnose Steve global` for the affected online player and channel. An available explicit channel format wins over a primary-group format, followed by the generic `chat` fallback. Check `use-group-formats`, duplicate file basenames, and reload errors. A saved personal chat color can override the format's base color. See [Chat Formats](configuration/chat-formats.md).

### Does a design preview change everyone's chat?

No. The gallery and editor preview only send a private sample. Staging a design is still an unsaved draft; **Save and apply** changes the selected format after creating a backup. Closing a normal editor view discards an unsaved draft. Use [Chat Style Editor](features/chat-style-editor.md) for restore and conflict rules.

### What does a player style profile save?

A profile saves personal chat color, name color, and selected tag. It does not save a nickname, rank, permissions, or a server layout. Switching rechecks current access. See [Player Style Profiles](features/player-style-profiles.md).

### PlaceholderAPI placeholders show as raw text

1. Check PlaceholderAPI is installed and `hooks.placeholder-api: true` in `config.yml`.
2. Use `%placeholder%` syntax for external expansions.
3. Install the required expansion if the provider needs one, then reload PlaceholderAPI as its documentation instructs.
4. Check [Placeholders](placeholders.md) for the actual LPC Pro placeholder names and Folia limits.

`strip-unresolved-placeholders: true` hides unresolved text; it does not install a missing expansion or fix its data source.

### Players can't use colors in chat

Template formatting, `/color` cosmetics, and formatting typed into a message use different permissions. Check the relevant nodes in [Chat Formatting & Colors](features/chat-formatting.md). The legacy `can-use-colors` field in `advanced/groups.yml` does not grant those permissions.

### How do I disable a feature?

Use its documented feature switch, and the top-level switch if one exists. Restart after changing a top-level `enable...` setting. Do not delete a file to disable a feature: its manager may recreate defaults.

| Feature | File | Main Feature Setting |
|---|---|---|
| Anti-spam/caps/advertising/swear | `moderation/moderation.yml` | The corresponding section's `enabled` |
| AI | `moderation/ai-filter.yml` | `enabled` |
| Cloud word lists | `moderation/cloud-filter.yml` | `enabled` |
| Public replies | `chat/public-replies.yml` | `enabled` |
| Personal receiving controls | `chat/settings.yml` | `enabled`; `public-chat-channels` selects eligible public channel IDs |
| Inventory/ender/shulker/coordinates | `advanced/variables.yml` | Their separate variable sections |
| Newcomers | `features/newcomer.yml` | `enabled` |
| Smart announcements | `features/smart-announcements.yml` | `enabled` |
| Periodic announcements | `features/servermessages.yml` | `announcements.enabled` |
| MOTD | `features/motd.yml` | `enabled`, plus `config.yml` `enable-motd` |
| Discord | `integration/discord.yml` | `enabled`, plus `config.yml` `enable-discord` |

Use each feature page for exact subordinate keys and dependencies.

### How do I change the default chat channel?

Edit the existing `settings` section in `chat/channels.yml`:

```yaml
settings:
  default-channel: "global"
```

Use a valid channel defined in that file. Check [Chat Channels](features/chat-channels.md) for manual selection, automatic focus, access permissions, and invalid-channel handling.

### Why can a player still see some messages after hiding public chat?

The public receiving setting applies only to the configured eligible unrestricted global channel. Private/local channels, PMs, staff tools, system notices, and other plugins' messages have their own paths. Game receiving preferences also leave personal rewards intact. See [Chat Settings](features/chat-settings.md).

### Why won't a public reply open?

Public replies default to off and require managed deletion, an eligible local global source, current permissions, and a still-valid delivered-message action. They are unavailable on Folia. Do not copy another player's token or use an expired source. See [Public Replies](features/public-replies.md).

### How do I allow my server's domain in chat?

Add the domain to the existing anti-advertising section in `moderation/moderation.yml`:

```yaml
anti-advertising:
  allowed-domains:
    - "yourserver.com"
    - "discord.gg"
```

Reload and test the intended message as a normal player. See [Anti-Advertising](moderation/anti-advertising.md) before broadly allowing shared host domains.

---

## Troubleshooting

### Plugin won't enable

Read the first LPC Pro startup error. Check the [server and Java requirements](getting-started/requirements.md), a single installed LPC Pro JAR, required runtime library downloads, and database/schema access. Fix the underlying error rather than repeatedly hot-loading the plugin.

### Database connection failed

Check the actual keys in [Database](configuration/database.md), connectivity, credentials, schema permissions, and UTF-8 support. Stop the server before changing storage mode or restoring data. Switching to an empty SQLite database can diagnose a connection issue in a **separate test copy**, but is not a migration of your existing records.

### Non-English characters appear garbled

Keep edited files in UTF-8 and use a Unicode-capable database configuration. If an older Java environment uses another default encoding, set it when starting that test/server process:

```sh
java -Dfile.encoding=UTF-8 -jar server.jar --nogui
```

Keep your normal memory and startup arguments as well. A resource pack or client font problem is separate from file/database encoding.

### Message deletion isn't working

Check [Message Deletion](moderation/message-deletion.md), its `advanced/message-deletion.yml` settings, the staff permission, and whether the source was stored by LPC Pro. ProtocolLib interception is a separate optional path; it does not make every packet or other plugin's message deletable. Folia disables managed deletion/replay.

### A shared inventory or shulker no longer opens

Shares are bounded snapshots with expiry, recipient checks, and source-session cleanup. Rejoining, reloading, disabling the feature, expiry, or capacity limits can invalidate them. Items cannot be taken from the viewer. Use [Inventory Sharing](features/inventory-sharing.md); Folia does not provide these viewers.

### Bedrock doesn't open the same chat actions as Java

Use `/chatmenu` for supported recent received-message actions and `/toggle menu` for settings on a genuine supported Geyser/Floodgate connection. Not every Java inventory menu is a native form. Check the provider's compatibility with the actual Bedrock version and transport. See [Geyser & Floodgate](integrations/geyser.md).

### Emojis or glyphs aren't rendering

Check the provider is installed, its hook is enabled, the exact glyph ID/syntax exists, and the client loaded the correct resource pack. ItemsAdder, Oraxen, and Nexo have different lookup behavior; multiple hooks are not a universal guarantee of interchangeable fonts. See their integration pages.

### AI is unavailable or leaves messages visible

AI is post-hoc, disabled by default, and permits messages when the provider is unavailable, queued beyond limits, or returns an unusable response. Observe deliberately performs no AI player punishment or deletion. Check `/lpc status`, endpoint/profile/backend, credentials, quotas, and the [AI guide](moderation/ai-filter.md). The moderation queue is not automatically populated by the normal AI pipeline.

### Saved settings appear unavailable

Check storage health in `/lpc status`. A loading/failed settings state is not a successful empty load. Resolve the storage problem and reconnect to reload durable settings; do not overwrite the database with guessed defaults.

### A command belongs to another plugin

Check LPC Pro's [command customization](configuration/command-customization.md) and `override-conflicting-commands` list. Verify the actual label/alias after reload and use the appropriate namespaced command while diagnosing a conflict.

### Getting “No permission” errors

Check both the command-level and action-specific nodes in [Commands & Permissions](commands-and-permissions.md). With LuckPerms, use `/lp user Steve permission check lpcpro.chatprofile` for a concrete effective permission check. Some runtime checks use nodes that have no declared default; grant those explicitly rather than assuming operator access.

### High memory usage or lag

Use `/lpc status` to check processing/delivery latency, storage queues, rejected writes, and provider health before changing settings. Review expensive placeholder expansions, enabled tasks, message rate, and audiences. Do not infer a player-capacity guarantee from a test count or assume that changing SQLite to MySQL alone fixes lag.
