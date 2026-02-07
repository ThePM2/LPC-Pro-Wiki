# PlaceholderAPI

LPC Pro integrates with [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/) in two ways: it **consumes** PAPI placeholders in chat formats, and it **provides** its own placeholders for other plugins to use.

## Setup

1. Install PlaceholderAPI on your server
2. Ensure `placeholder-api: true` is set in `config.yml` under `hooks:`

No additional setup is needed — LPC Pro automatically registers its expansion.

## Using PAPI Placeholders in LPC Pro

Any `%placeholder%` from PlaceholderAPI can be used in chat formats (`formats/*.yml`), hover tooltips, and server messages.

### Common Placeholders

| Placeholder | Source | Description |
|---|---|---|
| `%player_name%` | Player | Player's name |
| `%player_displayname%` | Player | Display name |
| `%player_first_join_date%` | Player | First join date |
| `%statistic_hours_played%` | Statistic | Hours played |
| `%server_online%` | Server | Online player count |
| `%vault_prefix%` | Vault | Player's prefix |
| `%luckperms_prefix%` | LuckPerms | Player's prefix |

### Example Usage in Chat Format

```yaml
player:
  text: "{prefix} {name}"
  hover:
    - "&8Joined %player_first_join_date%"
    - "&7Hours played: &f%statistic_hours_played%h"
    - "&7Balance: &f%vault_eco_balance%"
```

## LPC Pro Placeholders

LPC Pro provides the following placeholders for use in other plugins (scoreboard, TAB, etc.):

| Placeholder | Description |
|---|---|
| `%lpcpro_messages%` | Messages sent (formatted: 1.2K) |
| `%lpcpro_messages_raw%` | Messages sent (raw number) |
| `%lpcpro_mentions%` | Unique players mentioned (formatted: 1.2K) |
| `%lpcpro_replies%` | Replies sent (formatted: 1.2K) |
| `%lpcpro_polls%` | Polls voted in (formatted: 1.2K) |
| `%lpcpro_reputation%` | Reputation score |
| `%lpcpro_reputation_rank%` | Reputation leaderboard rank |
| `%lpcpro_achievements%` | Achievement progress (e.g., "5/15") |
| `%lpcpro_achievements_unlocked%` | Unlocked achievements count |
| `%lpcpro_achievements_total%` | Total achievements |
| `%lpcpro_achievements_percent%` | Unlock percentage (e.g., "33%") |
| `%lpcpro_balance%` | Shop currency balance |
| `%lpcpro_balance_formatted%` | Shop balance (formatted: 1.2K) |
| `%lpcpro_chatting_days%` | Days since first message |

See the full list on the [Placeholders](../placeholders.md) page.
