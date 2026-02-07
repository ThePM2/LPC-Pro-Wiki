# Chat Shop

LPC Pro includes a built-in cosmetics shop where players can spend currency on chat colors, name colors, tags, and perks. Configuration is in `features/shop.yml`.

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/chatshop` | `/cshop`, `/perkshop`, `/chatstore` | Open the shop GUI | `lpcpro.shop` |
| `/chatshop balance` | — | Check your currency balance | `lpcpro.shop` |
| `/chatshop colors` | — | Browse chat colors | `lpcpro.shop` |
| `/chatshop names` | — | Browse name colors | `lpcpro.shop` |
| `/chatshop tags` | — | Browse tags | `lpcpro.shop` |
| `/chatshop perks` | — | Browse perks | `lpcpro.shop` |
| `/chatshop give <player> <amount>` | — | Give currency to a player | `lpcpro.shop.admin` |
| `/chatshop set <player> <amount>` | — | Set a player's balance | `lpcpro.shop.admin` |
| `/chatshop take <player> <amount>` | — | Take currency from a player | `lpcpro.shop.admin` |

## Currency Modes

The shop supports three currency backends:

```yaml
# Currency mode: points, vault, item
currency-mode: "points"

# Currency display name
currency-name: "Points"
```

| Mode | Description |
|---|---|
| `points` | Internal LPC Pro points system (default) |
| `vault` | Uses Vault economy (requires Vault + economy plugin) |
| `item` | Uses items as currency |

## Configuration

```yaml
# Pagination settings
pagination:
  items-per-page: 21   # Max items per page (1-21)
```

Set `items-per-page` lower to split categories across multiple pages:
- `21` — All 3 rows, no pagination unless category exceeds 21 items
- `14` — 2 rows per page
- `7` — 1 row per page

## Permissions

| Permission | Description |
|---|---|
| `lpcpro.shop` | Access the chat shop |
| `lpcpro.shop.admin` | Manage shop currency (give/set/take) |

## PlaceholderAPI

| Placeholder | Description |
|---|---|
| `%lpcpro_balance%` | Player's shop currency balance |
| `%lpcpro_balance_formatted%` | Formatted balance (e.g., 1.2K) |
