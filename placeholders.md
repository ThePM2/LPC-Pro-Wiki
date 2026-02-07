# Placeholders

LPC Pro provides two types of placeholders: **built-in placeholders** for use in chat format files, and **PlaceholderAPI placeholders** for use in other plugins.

## Built-in Placeholders

These placeholders work in chat format files (`formats/*.yml`) without any additional plugins:

### Player Placeholders

| Placeholder | Description |
|---|---|
| `{name}` | Player name (with nickname if set) |
| `{player}` | Same as `{name}` |
| `{nickname}` | Player's nickname (or real name if not set) |
| `{displayname}` | Player's display name |
| `{prefix}` | Rank prefix (from Vault/LuckPerms) |
| `{suffix}` | Rank suffix |
| `{tag}` | Active chat tag (includes leading space when set) |
| `{world}` | Player's current world |

### Message Placeholders

| Placeholder | Description |
|---|---|
| `{message}` | The chat message content |

### Private Message Placeholders

| Placeholder | File | Description |
|---|---|---|
| `{receiver_name}` | `msg-sender.yml` | Recipient's name |
| `{sender_name}` | `msg-receiver.yml` | Sender's name |

### Server Message Placeholders

| Placeholder | File | Description |
|---|---|---|
| `{player}` | `servermessages.yml` | Player who joined/quit/died |
| `{killer}` | Death messages | PvP killer name |
| `{mob}` | Death messages | Mob name |
| `{reason}` | Clear chat | Reason provided |

### Tab List Placeholders

| Placeholder | Description |
|---|---|
| `{player}` | Player name |
| `{displayname}` | Player display name |
| `{online}` | Online player count |
| `{max}` | Max player slots |
| `{tps}` | Server TPS |
| `{ping}` | Player ping (ms) |
| `{world}` | Current world name |
| `{time}` | Server time (HH:mm) |
| `{rank}` | Primary group |

---

## PlaceholderAPI Placeholders

These placeholders require [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/) and work both within LPC Pro formats and in other plugins (scoreboards, TAB, holograms, etc.).

### LPC Pro Expansion

| Placeholder | Description |
|---|---|
| `%lpcpro_messages%` | Messages sent (formatted: 1.2K, 3.5M) |
| `%lpcpro_messages_raw%` | Messages sent (raw number) |
| `%lpcpro_mentions%` | Unique players mentioned (formatted: 1.2K, 3.5M) |
| `%lpcpro_replies%` | Replies sent (formatted: 1.2K, 3.5M) |
| `%lpcpro_polls%` | Polls voted in (formatted: 1.2K, 3.5M) |
| `%lpcpro_reputation%` | Reputation score |
| `%lpcpro_reputation_rank%` | Reputation leaderboard rank |
| `%lpcpro_achievements%` | Achievement progress (e.g., "5/15") |
| `%lpcpro_achievements_unlocked%` | Unlocked achievements count |
| `%lpcpro_achievements_total%` | Total achievements count |
| `%lpcpro_achievements_percent%` | Unlock percentage (e.g., "33%") |
| `%lpcpro_balance%` | Shop currency balance |
| `%lpcpro_balance_formatted%` | Shop balance (formatted: 1.2K, 3.5M) |
| `%lpcpro_chatting_days%` | Days since first message |

### Using in Chat Formats

PlaceholderAPI placeholders can be used directly in `text` and `hover` fields:

```yaml
player:
  text: "{prefix} {name}"
  hover:
    - "&8Joined %player_first_join_date%"
    - "&7Hours played: &f%statistic_hours_played%h"
    - "&7Messages: &f%lpcpro_messages%"
    - "&bReputation: &f%lpcpro_reputation% &8(#%lpcpro_reputation_rank%)"
    - "&7Achievements: &f%lpcpro_achievements% &8(%lpcpro_achievements_percent%)"
```

### Popular Third-Party Placeholders

| Placeholder | Plugin | Description |
|---|---|---|
| `%player_name%` | Player | Player name |
| `%player_first_join_date%` | Player | First join date |
| `%statistic_hours_played%` | Statistic | Hours played |
| `%server_online%` | Server | Online count |
| `%vault_prefix%` | Vault | Rank prefix |
| `%vault_eco_balance%` | Vault | Economy balance |
| `%luckperms_prefix%` | LuckPerms | LuckPerms prefix |
| `%luckperms_primary_group_name%` | LuckPerms | Primary group |

For the full list of available PlaceholderAPI placeholders, see the [PlaceholderAPI wiki](https://github.com/PlaceholderAPI/PlaceholderAPI/wiki/Placeholders).
