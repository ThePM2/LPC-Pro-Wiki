# ❓ FAQ & Troubleshooting

## Frequently Asked Questions

### How do I reload the plugin?

Use `/lpc reload` to reload all configuration files. Note that `database.yml` changes and private message toggles require a full server restart.

### Chat format changes aren't showing up

1. Make sure you edited the correct format file in `formats/`
2. Run `/lpc reload`
3. If using group-specific formats, check that the file name in `formats/groups/` matches the player's LuckPerms/Vault primary group name

### PlaceholderAPI placeholders show as raw text

1. Verify PlaceholderAPI is installed and running: `/papi list`
2. Check that `placeholder-api: true` is set in `config.yml` under `hooks:`
3. Make sure you're using `%placeholder%` syntax (not `{placeholder}`)
4. Some placeholders require additional expansion downloads: `/papi ecloud download <expansion>`

### Players can't use colors in chat

Color permissions are controlled in two places:

1. **advanced/groups.yml** — Set `can-use-colors: true` for the group
2. **Individual permissions** — Grant `lpcpro.color.<color>` or `lpcpro.color.*`

### The swear filter is too aggressive / not aggressive enough

- **Too aggressive**: Remove words from the `blocked-words` list in `moderation/moderation.yml`
- **Not aggressive enough**: Add more words to the list. Evasion detection (leet speak, separators, repeated chars) is automatic for every listed word.

### How do I disable a feature?

Most features have an `enabled:` toggle in their config file:

| Feature | File | Toggle |
|---|---|---|
| Anti-Spam | `moderation/moderation.yml` | `anti-spam.enabled` |
| Anti-Caps | `moderation/moderation.yml` | `anti-caps.enabled` |
| Anti-Advertising | `moderation/moderation.yml` | `anti-advertising.enabled` |
| Swear Filter | `moderation/moderation.yml` | `swear-filter.enabled` |
| Infractions | `moderation/moderation.yml` | `infractions.enabled` |
| Achievements | `features/achievements.yml` | `enabled` |
| Reputation | `features/reputation.yml` | `enabled` |
| Polls | `features/polls.yml` | `enabled` |
| Chat Games | `features/games.yml` | `enabled` |
| Mail | `features/mail.yml` | `enabled` |
| Tab List | `features/tablist.yml` | `enabled` |
| Newcomer System | `features/newcomer.yml` | `enabled` |
| Anti-Bot | `moderation/antibot.yml` | `enabled` |
| Discord | `integration/discord.yml` | `enabled` |
| Translation | `translation.yml` | `enabled` |
| Offline Messages | `features/offlinemessages.yml` | `enabled` |
| Smart Announcements | `features/smart-announcements.yml` | `enabled` |
| MOTD | `features/motd.yml` | `enabled` |
| Raid Protection | `moderation/raidprotection.yml` | `enabled` |
| Shop | `features/shop.yml` | (remove file to disable) |

### How do I change the default chat channel?

Edit `chat/channels.yml`:

```yaml
settings:
  default-channel: "global"  # Change to your preferred channel name
```

### How do I set up per-group chat formats?

1. Create a format file at `formats/groups/<groupname>.yml`
2. The file name must match the player's LuckPerms/Vault primary group name
3. Use the same format structure as `formats/chat.yml`
4. Run `/lpc reload`

### Private messages are disabled

Check `config.yml`:

```yaml
enable-private-messages: true
```

This setting requires a **server restart** to take effect.

### How do I allow my server's IP/domain in chat?

Add it to the allowed domains list in `moderation/moderation.yml`:

```yaml
anti-advertising:
  allowed-domains:
    - "yourserver.com"
    - "discord.gg"
```

---

## Troubleshooting

### Plugin won't enable

- Check your server console for error messages
- Verify your Java version meets your server's requirements (`java -version`)
- Verify you're running Paper or Spigot 1.17+
- Check for conflicting plugins

### Database connection failed

- Verify your MySQL credentials in `database.yml`
- Ensure the database exists with `utf8mb4_unicode_520_ci` collation
- Check that your MySQL server is accessible from the Minecraft server
- Try `type: local` (SQLite) to verify the issue is database-related

### Non-English characters appear garbled

Add `-Dfile.encoding=UTF-8` to your server's startup flags:

```bash
java -Dfile.encoding=UTF-8 -jar server.jar
```

For MySQL, ensure the database uses `utf8mb4` character set.

### Message deletion not working

- Verify ProtocolLib is installed and up to date
- Check that `protocol-lib: true` is set in `config.yml`
- Verify the player has `lpcpro.chat.delete` permission

### Emojis / Glyphs not rendering

- Verify ItemsAdder or Oraxen is installed
- Check the corresponding hook is enabled in `config.yml`
- Make sure emoji/glyph names match exactly (including case)
- Don't enable both ItemsAdder and Oraxen simultaneously

### Getting "No permission" errors

- Check that permission nodes match between your permission plugin and LPC Pro
- Use `/lp user <player> permission check <permission>` to debug LuckPerms permissions
- Review the [Commands & Permissions](commands-and-permissions.md) page for correct permission nodes

### High memory usage or lag

- If using SQLite, consider switching to MySQL for larger servers
- Increase the tab list `update-interval-ticks` value to reduce update frequency
- Disable features you don't use
- Check that `auto-game-interval-minutes` isn't set too low
