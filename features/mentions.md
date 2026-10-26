# 📌 Mentions

Players can mention others using `@username`. Eligible recipients see highlighted names and can receive a sound and title. Configuration is in `plugins/LPC-Pro/chat/mentions.yml`.

## Usage

| Syntax | Description | Permission |
|---|---|---|
| `@PlayerName` | Mention an eligible player | `lpcpro.mention` |
| `@everyone` | Mention the eligible message audience | `lpcpro.mention.everyone` |
| `@here` | Mention eligible recipients in the same world | `lpcpro.mention.everyone` |

Operators can use the special mentions. In 2.6.0, `@here` uses the same permission check as `@everyone`; `lpcpro.mention.here` is not a separate access check. `@here` is unavailable on Folia.

A mention does not bypass channel access, range, ignore, visibility or personal receiving preferences. Effects and credit are limited to the authorized audience of the new message. Quoted text in a [public reply](public-replies.md) does not trigger mentions again.

## Configuration

```yaml
enabled: true
color: "YELLOW"
bold: false
italic: false
underlined: true

sound:
  enabled: true
  name: "entity.experience_orb.pickup"
  volume: 1.0
  pitch: 1.0

title:
  enabled: true
  fade-in: 10
  stay: 40
  fade-out: 10

everyone:
  enabled: true
here:
  enabled: true
```

The `title` timing values are ticks. The main `config.yml` switch `enable-mentions` must also be enabled.

## Styling

| Setting | Type | Default | Description |
|---|---|---|---|
| `color` | string | `YELLOW` | Highlight color |
| `bold` | boolean | `false` | Bold mention text |
| `italic` | boolean | `false` | Italic mention text |
| `underlined` | boolean | `true` | Underline mention text |

## Mention Limits

The active newcomer policy can restrict the number of unique eligible recipients mentioned in a channel message. Repeated names count once; special mentions expand to their eligible audience.

The `max-mentions` fields in `advanced/groups.yml` remain in the configuration but are not enforced by the ordinary channel mention path in 2.6.0. Use the newcomer restrictions below where applicable; do not rely on a group field as a general mention cap.

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.mention` | `true` | Mention other players |
| `lpcpro.mention.receive` | `true` | Receive mention effects |
| `lpcpro.mention.everyone` | `op` | Use `@everyone` and `@here` |
| `lpcpro.toggle` | `true` | Change personal mention and sound preferences |

Players can use `/toggle mentions` to stop mention notifications. [Mention sounds](mention-sounds.md) provide a separate choice of the server tone, chime, bell or silence. Choosing silence keeps eligible highlighting and titles.

## Newcomer Restrictions

Merge the following into `features/newcomer.yml` to enable a one-recipient cap while a player is a newcomer:

```yaml
enabled: true
mention-restriction: true
max-mentions-per-message: 1
```

`-1` means unlimited and `0` means no eligible recipients. An over-cap message is rejected before effects and delivery. Normal moderation and attempted-message cooldown may already have run.

`lpcpro.newcomer.bypass` bypasses newcomer restrictions. `lpcpro.slowmode.bypass` bypasses delays only; it does not bypass the mention cap.
