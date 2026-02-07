# 📄 Content Filter

The content filter extends LPC Pro's chat moderation to non-chat content: signs, books, and anvil item renames. It reuses the same filters configured in `moderation/moderation.yml` (swear filter, anti-advertising, etc.). Configuration is in `moderation/content-filter.yml`.

## Configuration

```yaml
# Apply chat filters to sign text
filter-signs: true

# Apply chat filters to book content
filter-books: true

# Apply chat filters to anvil item renames
filter-anvil: true

# true = Block the action entirely
# false = Allow but censor the content (replace bad words with ***)
block-on-filter: true
```

## Filter Behavior

| Mode | Behavior |
|---|---|
| `block-on-filter: true` | The action is cancelled — sign won't place, book won't save, item won't rename |
| `block-on-filter: false` | The content is allowed but bad words are replaced with `***` |

## What Gets Filtered

The content filter applies all active moderation filters from `moderation/moderation.yml`:

- **Swear filter** — Blocked words and evasion detection
- **Anti-advertising** — URLs, IPs, and domains
- Any other active chat filters

## Bypass Permissions

Staff can bypass content filtering per content type:

| Permission | Description |
|---|---|
| `lpcpro.bypass.filter.sign` | Bypass sign content filter |
| `lpcpro.bypass.filter.book` | Bypass book content filter |
| `lpcpro.bypass.filter.anvil` | Bypass anvil rename filter |
