# 🛡️ Moderation Overview

LPC Pro includes a comprehensive moderation suite for keeping your server chat clean and safe. All moderation features are configured in `moderation/moderation.yml` unless noted otherwise.

## Moderation Features

### Chat Filters

Automatic filters that process every chat message:

| Filter | Config File | Description |
|---|---|---|
| [Anti-Spam](anti-spam.md) | `moderation/moderation.yml` | Message cooldown and similarity detection |
| [Anti-Caps](anti-caps.md) | `moderation/moderation.yml` | Excessive capitals enforcement |
| [Anti-Advertising](anti-advertising.md) | `moderation/moderation.yml` | URL, IP, and domain blocking |
| [Swear Filter](swear-filter.md) | `moderation/moderation.yml` | Profanity filtering with evasion detection |
| [AI Filter](ai-filter.md) | `moderation/ai-filter.yml` | AI-powered content analysis via OpenAI |
| [Cloud Filter](cloud-filter.md) | `moderation/cloud-filter.yml` | Cloud-sourced word list filtering |
| [Content Filter](content-filter.md) | `moderation/content-filter.yml` | Filter signs, books, and anvil renames |

### Staff Tools

Manual moderation commands for staff:

| Tool | Description |
|---|---|
| [Muting](muting.md) | Mute players, channels, or the entire server |
| [Warnings](warnings.md) | Warn players with automatic threshold actions |
| [Reports](reports.md) | Player reporting system |
| [Infractions](infractions.md) | Automatic infraction point tracking |
| [Mod Queue](mod-queue.md) | Staff review queue for flagged messages |

### Protection Systems

| System | Config File | Description |
|---|---|---|
| [Anti-Bot](anti-bot.md) | `moderation/antibot.yml` | Bot detection and rate limiting |
| [Newcomer System](newcomer-system.md) | `features/newcomer.yml` | Special handling for new players |
| [Raid Protection](raid-protection.md) | `moderation/raidprotection.yml` | Mass-join flood protection |

## Processing Pipeline

When a player sends a chat message, it passes through this pipeline:

1. **Slowmode Check** — Enforce channel slowmode
2. **Raid Protection** — Check if raid mode restricts this player
3. **Mute Check** — Block if player or channel is muted
4. **Channel Permission** — Verify player can speak in this channel
5. **Anti-Bot** — Check if player meets chat cooldown requirements
6. **Chat Game** — Intercept message if a chat game is active
7. **Moderation Filters** — Run the following filters in order:
   - **Anti-Spam** — Check message delay and similarity
   - **Anti-Advertising** — Check for URLs and IPs
   - **Swear Filter** — Check for blocked words and patterns
   - **Anti-Caps** — Check caps percentage
   - **Cloud Filter** — Check against remote word lists
   - **AI Filter** — Optional AI-powered content analysis (async)

If a message fails any filter, the configured action is taken (cancel, warn, censor, etc.). Infraction points are tracked inline when filter violations are detected.

## Bypass Permissions

Each filter has a bypass permission for staff:

| Permission | Bypasses |
|---|---|
| `lpcpro.bypass.spam` | Anti-spam filter |
| `lpcpro.bypass.caps` | Anti-caps filter |
| `lpcpro.bypass.advertising` | Anti-advertising filter |
| `lpcpro.bypass.filter` | Swear/profanity filter |
| `lpcpro.bypass.grammar` | Auto grammar corrections |
| `lpcpro.bypass.mute` | Mute restrictions |
| `lpcpro.slowmode.bypass` | Channel slowmode |

{% hint style="warning" %}
The `bypass-moderation` group property in `advanced/groups.yml` is loaded from config but is **not currently checked** by the moderation pipeline. Use the individual bypass permissions above to grant filter bypass to staff.
{% endhint %}

## Staff Spy

Staff can monitor messages that were silently filtered:

| Permission | Description |
|---|---|
| `lpcpro.spy.silent` | See messages that were cancelled by filters (visible only to sender) |
| `lpcpro.spy.pm` | See all private messages |
| `lpcpro.spy.channel` | See messages in all channels |

## Message Deletion

With ProtocolLib installed, staff can delete individual messages from chat:

| Permission | Description |
|---|---|
| `lpcpro.chat.delete` | Click the `[X]` button to delete any message |

Messages are removed from the chat window of all players who received them.
