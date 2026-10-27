# 🏷️ Tags

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

Higher tier takes precedence when no manual tag is selected — a player with both `lpcpro.autotag.mod` and `lpcpro.autotag.admin` falls back to the Admin tag. A valid manual selection takes precedence over an auto-tag. Set `enable-auto-tag: false` in `config.yml` to stop automatic tags while keeping manual selection; changing this main switch requires a restart.

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


## Access and Saved Selection

Definitions live in `chat/tags.yml`. `enable-tags: false` in `config.yml` disables tag rendering and its command, including manual and automatic tags. That main switch requires a restart; reload tag definitions with `/lpc reload`.

The `/tags` command needs `lpcpro.tags`, which is not explicitly defaulted to all players in the plugin descriptor. Grant it to the intended group. A tag itself can be available through its configured permission, an earned achievement reward or an owned shop unlock. Menu selection, applying a saved style profile and normal chat rendering check current access.

If a selected tag is removed from the catalog or its permission/unlock is no longer available, it stops appearing. The player's current auto-tag is used instead, or no tag if none applies. The saved manual choice is kept, so it can return when access is restored; use the menu's reset action to clear it deliberately.

Rendering uses already loaded achievement and shop ownership state without starting a database read. If that state is not available yet, it does not assume that the reward is unlocked. Confirmed shop ownership can still provide a tag without access to the general tag menu, including an owned offer that has been disabled for new purchases.

```text
/lp group default permission set lpcpro.tags true
/lp group moderator permission set lpcpro.tag.mod true
/lp group moderator permission set lpcpro.autotag.mod true
```

The first node opens the menu, the second allows manual use of the Mod tag, and the third supplies its automatic fallback. Manual selection is saved in player settings. Tags can also be included in a [Style Profile](player-style-profiles.md), with current access checked when applying the profile.
