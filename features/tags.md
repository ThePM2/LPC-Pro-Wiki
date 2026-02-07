# Tags

Tags are cosmetic labels displayed in chat next to a player's name. Tags can be earned through achievements, purchased from the chat shop, or automatically assigned based on staff permissions.

## Commands

| Command | Description |
|---|---|
| `/tags` | Open the tags GUI to select a tag (aliases: `/tag`, `/chattags`, `/nametag`) |

**Permission:** `lpcpro.tags`

## Auto-Tags

Staff members can have tags automatically assigned based on their rank permission:

| Permission | Tag | Tier |
|---|---|---|
| `lpcpro.autotag.staff` | Staff | 1 (lowest) |
| `lpcpro.autotag.helper` | Helper | 2 |
| `lpcpro.autotag.trial-mod` | Trial-Mod | 3 |
| `lpcpro.autotag.mod` | Mod | 4 |
| `lpcpro.autotag.admin` | Admin | 5 |
| `lpcpro.autotag.owner` | Owner | 6 (highest) |

Higher tier takes precedence — a player with both `lpcpro.autotag.mod` and `lpcpro.autotag.admin` will display the Admin tag.

## Manual Tag Permissions

Players can manually select tags they have permission for:

| Permission | Tag |
|---|---|
| `lpcpro.tag.staff` | Staff |
| `lpcpro.tag.helper` | Helper |
| `lpcpro.tag.trial-mod` | Trial-Mod |
| `lpcpro.tag.mod` | Mod |
| `lpcpro.tag.admin` | Admin |
| `lpcpro.tag.owner` | Owner |

## Achievement Tags

Achievements can grant tags as rewards. See [Achievements](achievements.md) for details. Examples:

- `[Chatterbox]` — Send 100 messages
- `[Veteran]` — Send 1,000 messages
- `[Respected]` — Reach 10 reputation

## Format Integration

The `{tag}` placeholder in chat formats displays the player's active tag:

```yaml
player:
  text: "{prefix}{tag} {name}"
```

The `{tag}` placeholder includes a leading space when set, so formatting remains clean even for players without tags.
