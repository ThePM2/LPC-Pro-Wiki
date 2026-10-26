# 🛡️ Moderation Overview

LPC Pro includes automatic chat filters and staff tools for managing chat. Most local filter settings are in `moderation/moderation.yml`; optional systems have their own files.

## Moderation Features

### Chat Filters

| Filter | Config File | Description |
|---|---|---|
| [Anti-Spam](anti-spam.md) | `moderation/moderation.yml` | Message cooldown and similarity detection |
| [Anti-Caps](anti-caps.md) | `moderation/moderation.yml` | Excessive capitals enforcement |
| [Anti-Advertising](anti-advertising.md) | `moderation/moderation.yml` | URL, IP, and domain blocking |
| [Swear Filter](swear-filter.md) | `moderation/moderation.yml` | Local profanity filtering with evasion detection |
| [AI Filter](ai-filter.md) | `moderation/ai-filter.yml` | Optional post-hoc analysis, Observe or Enforce |
| [Cloud Filter](cloud-filter.md) | `moderation/cloud-filter.yml` | Downloaded word lists and local additions |
| [Content Filter](content-filter.md) | `moderation/content-filter.yml` | Filter signs, books, and anvil renames |

### Staff Tools

| Tool | Description |
|---|---|
| [Muting](muting.md) | Mute players, channels, or the server |
| [Warnings](warnings.md) | Issue manual warnings with point thresholds |
| [Reports](reports.md) | Review player reports and their captured context |
| [Infractions](infractions.md) | Track automatic moderation points |
| [Message Deletion](message-deletion.md) | Remove retained, managed chat messages |
| [Slowmode](slowmode.md) | Set a manual chat delay |
| [Mod Queue](mod-queue.md) | Manage queued entries; built-in filters do not currently populate it |

Staff can also use `/note add <player> <note>`, `/note list <player>`, `/note remove <id>`, and `/note clear <player>`. These require `lpcpro.note` and the corresponding `.add`, `.view`, `.remove`, or `.clear` permission. `lpcpro.note.notify` allows join notifications about staff notes.

### Protection Systems

| System | Config File | Description |
|---|---|---|
| [Anti-Bot](anti-bot.md) | `moderation/antibot.yml` | Join cooldowns and bot-like chat detection |
| [Newcomer System](newcomer-system.md) | `features/newcomer.yml` | Optional persistent newcomer policy |
| [Raid Protection](raid-protection.md) | `moderation/raidprotection.yml` | Join/message spike detection and temporary restrictions |

## Processing Pipeline

Channel access, membership, mutes, slowmode, newcomer state, raid restrictions, and anti-bot checks can prevent a message before normal formatting and delivery. A successful chat-game answer may also be consumed by the game.

Within the normal moderation filter stage, the order is:

1. **Anti-Spam** — Check normal message delay and similarity.
2. **Anti-Advertising** — Check URLs and IPs.
3. **Swear Filter** — Cancel, warn, or censor local matches.
4. **Anti-Caps** — Check the uppercase percentage.
5. **Cloud Filter** — Censor matches from the separate cloud/local list.
6. **AI Filter** — Submit optional analysis in the background.

Earlier rejection stops the remaining filter stages. Accepted text can be displayed before an AI result. Private messages use the local swear filter when enabled, rather than every normal-chat filter. Content filtering skips chat anti-spam.

## Bypass Permissions

| Permission | Bypasses |
|---|---|
| `lpcpro.bypass.spam` | Normal anti-spam delay and similarity |
| `lpcpro.bypass.cooldown.partial` | Reduces the normal delay, without removing similarity checks |
| `lpcpro.bypass.caps` | Anti-caps |
| `lpcpro.bypass.advertising` | Anti-advertising |
| `lpcpro.bypass.filter` | Local swear filter |
| `lpcpro.bypass.aifilter` | AI submission |
| `lpcpro.bypass.grammar` | Grammar correction |
| `lpcpro.bypass.mute` | Mute restrictions |
| `lpcpro.slowmode.bypass` | Applicable slowmode delay |
| `lpcpro.bypass.antibot` | Anti-bot checks |
| `lpcpro.raidmode.bypass` | Raid restrictions |
| `lpcpro.newcomer.bypass` | Newcomer policy |

The cloud filter is configured independently; the local swear-filter bypass does not disable it. Group fields such as `bypass-moderation` and `bypass-mute` do not replace the individual permissions above.

## Staff Spy

| Command | Permission | Description |
|---|---|---|
| `/spy` | `lpcpro.spy.pm` | Toggle private-message spying |
| `/channelspy <channel>` | `lpcpro.spy.channel` | Toggle spying for that channel; no argument lists current status |
| `/commandspy` | `lpcpro.spy.command` | Toggle command spying |

`lpcpro.spy.silent` allows the separate staff copy of silently cancelled messages. Spy access is sensitive: grant it only to trusted staff and review exclusions in `advanced/command-spy.yml`.

## Reload and Health

Use `/lpc reload` after editing feature files and `/lpc status` to check their health. Both require `lpcpro.admin`; reload also requires `lpcpro.command.reload`. Changes to top-level `enable-...` settings in `config.yml` require a restart. On Folia, individual message deletion, public replies, and inventory/shulker viewers are unavailable; range/same-world channels and chat bubbles also have restrictions.
