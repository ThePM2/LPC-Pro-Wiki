# 🧩 PlaceholderAPI

LPC Pro consumes PlaceholderAPI values in its text and registers its own expansion for other plugins. Internal `%lpcpro_*%` values also resolve inside LPC without installing PlaceholderAPI.

## Setup

1. Install PlaceholderAPI and keep `hooks.placeholder-api: true` in `config.yml`.
2. Install the expansions required by your chosen external placeholders.
3. Reload PlaceholderAPI after installing expansions.

For the common Player, Statistic, and Server values:

```text
/papi ecloud download player
/papi ecloud download statistic
/papi ecloud download server
/papi reload
```

LPC Pro warns about missing common expansions; it does not download them automatically. Its own expansion registers automatically when the hook is active.

## Using PAPI Placeholders in LPC Pro

Installed external placeholders can be used in chat formats, hover tooltips, and supported server messages. Missing expansions may leave unresolved text. `strip-unresolved-placeholders: true` in `config.yml` removes unresolved `%...%` text rather than installing an expansion.

| Placeholder | Required Source | Description |
|---|---|---|
| `%player_name%` | Player expansion | Account name |
| `%player_displayname%` | Player expansion | Display name |
| `%player_first_join_date%` | Player expansion | First join date |
| `%statistic_hours_played%` | Statistic expansion | Played hours |
| `%server_online%` | Server expansion | Online count |
| `%vault_prefix%` | Vault expansion and provider | Rank prefix |
| `%luckperms_prefix%` | LuckPerms expansion | LuckPerms prefix |

### Example Usage in Chat Format

```yaml
player:
  text: "{prefix} {name}"
  hover:
    - "<gray>Messages: <white>%lpcpro_messages%</white>"
    - "<gray>Hours played: <white>%statistic_hours_played%</white>"
```

This is a format part; keep the rest of your existing format. External values depend on the installed expansion and its configuration. Avoid slow network-backed placeholders on every chat message.

## LPC Pro Placeholders

| Placeholder | Description |
|---|---|
| `%lpcpro_messages%` | Formatted message count |
| `%lpcpro_messages_raw%` | Raw message count |
| `%lpcpro_mentions%` | Unique eligible players mentioned |
| `%lpcpro_replies%` | Reply count |
| `%lpcpro_polls%` | Poll vote count |
| `%lpcpro_reputation%` | Reputation score |
| `%lpcpro_reputation_rank%` | Reputation rank |
| `%lpcpro_achievements%` | Unlocked/total achievements |
| `%lpcpro_achievements_unlocked%` | Unlocked count |
| `%lpcpro_achievements_total%` | Total count |
| `%lpcpro_achievements_percent%` | Unlock percentage |
| `%lpcpro_balance%` | Current shop balance |
| `%lpcpro_balance_formatted%` | Formatted balance |
| `%lpcpro_chatting_days%` | Days since the first recorded message |
| `%lpcpro_settings_ready%` | Whether the player's settings are loaded |
| `%lpcpro_settings_public_chat%` | Saved public-chat receiving choice |
| `%lpcpro_settings_games%` | Saved chat-game receiving choice |

Settings preferences can return `unavailable` while the snapshot is not loaded. See the full [Placeholders](../placeholders.md) reference for tags, nicknames, receiving controls, and all preference keys. Other plugins need PlaceholderAPI to consume these values through its API.
