# 🔤 Placeholders

LPC Pro provides **built-in format placeholders** and its own **`%lpcpro_*%` placeholders**. Both work inside LPC Pro without PlaceholderAPI. Install PlaceholderAPI to use third-party expansions or resolve LPC Pro placeholders from other plugins.

## Built-in Placeholders

These placeholders work in chat format files (`formats/*.yml`) without any additional plugins:

### Player Placeholders

| Placeholder | Description |
|---|---|
| `{name}` | Player name (with nickname if set) |
| `{player}` | Same as `{name}` |
| `{sender_name}` | Effective sender name, also available in private-message formats |
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
| `{blank}` / `{empty}` | An empty text fragment |

`<nl>` inserts a newline in a text/hover field. Built-in placeholders are context-specific: a tab list placeholder is not automatically a chat format placeholder.

### Private Message Placeholders

| Placeholder | File | Description |
|---|---|---|
| `{receiver_name}` | `msg-sender.yml` | Recipient's name |
| `{sender_name}` | `msg-receiver.yml` | Sender's name |

### Server Message Placeholders

| Placeholder | File | Description |
|---|---|---|
| `{player}` | `features/servermessages.yml` | Player who joined/quit/died |
| `{killer}` | Death messages | PvP killer name |
| `{mob}` | Death messages | Mob name |
| `{reason}` | Clear-chat message template | Reason provided |

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

The LPC Pro expansion is registered automatically when [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/) is installed and its hook is enabled. There is no separate LPC Pro eCloud download. LPC Pro also resolves its own placeholders internally when PlaceholderAPI is absent.

Third-party placeholders such as `%player_name%` still need PlaceholderAPI and the matching expansion. Unrecognized placeholders are normally left visible; `strip-unresolved-placeholders: true` in `config.yml` removes unresolved `%word%` tokens from chat formats.

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
| `%lpcpro_tag%` | Effective online chat tag, converted to legacy section-color codes |
| `%lpcpro_tag_raw%` | Effective online tag as MiniMessage |
| `%lpcpro_tag_plain%` | Effective online tag with formatting removed |
| `%lpcpro_nickname%` | LPC nickname as legacy section-color text, or real name |
| `%lpcpro_nickname_raw%` | Safe LPC nickname markup, or real name |
| `%lpcpro_nickname_plain%` | LPC nickname with formatting removed, or real name |
| `%lpcpro_settings_ready%` | `true` when the player's settings are loaded |
| `%lpcpro_settings_controls_available%` | `true` when receiving controls are enabled and ready |
| `%lpcpro_settings_public_chat%` | Stored public-chat preference: `true`, `false` or `unavailable` |
| `%lpcpro_settings_games%` | Stored game-message preference: `true`, `false` or `unavailable` |
| `%lpcpro_settings_pm%` | Private-message preference |
| `%lpcpro_settings_dnd%` | DND preference (`true` means DND is on) |
| `%lpcpro_settings_mentions%` | Mention preference |
| `%lpcpro_settings_sounds%` | Sound preference |
| `%lpcpro_settings_join%` | Join-message preference |
| `%lpcpro_settings_quit%` | Quit-message preference |
| `%lpcpro_settings_death%` | Death-message preference |

Settings values report the saved preference, not proof that every kind of message is filtered. All settings preferences return `unavailable` while the player's settings are loading or unavailable. Tags and nicknames need an online player for their active cosmetic state; offline tags are empty and offline nicknames fall back to the real name. Balance is `0` for offline players. Other values can fall back to `0` or `?` when their backing feature is unavailable.

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


## Chat Sharing Variables

Players type these into local channel chat; they are separate from format placeholders and PlaceholderAPI.

| Variable | Description | Permission |
|---|---|---|
| `[item]` / `[i]` | Show the held item's tooltip; a shulker can open a frozen content preview | `lpcpro.variable.item` |
| `[inv]` | Share a frozen inventory preview | `lpcpro.variable.inv` |
| `[ender]` | Share a frozen personal ender chest preview | `lpcpro.variable.ender` |
| `[coords]` | Share the current world and block coordinates with a copy action | `lpcpro.variable.coords` |

Preview links are only usable by recipients to whom the message was delivered in the current session. Inventory, ender chest and shulker previews are read-only and expire; they do not expose a live inventory. These viewers are unavailable on Folia. Copy actions depend on client support; a Bedrock client does not offer the same clipboard action as Java.

## Relational Placeholders

On ordinary Paper/Spigot servers, chat formats can also resolve PlaceholderAPI relational placeholders against the sender and each recipient. Folia does not resolve these pairwise placeholders because another player's state may belong to a different region. Use sender-only or literal fallbacks for Folia formats.
