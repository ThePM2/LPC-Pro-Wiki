# 🛒 Chat Shop

LPC Pro includes a cosmetics shop for chat colors, name colors, tags and supported perks. Configuration is in `plugins/LPC-Pro/features/shop.yml`. Purchases and internal point balances are stored in the configured database.

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/chatshop` | `/cshop`, `/perkshop`, `/chatstore` | Open the shop | `lpcpro.shop` |
| `/chatshop balance` | `bal`, `points` subcommands | Check the current currency balance | `lpcpro.shop` |
| `/chatshop colors` | — | Browse chat colors | `lpcpro.shop` |
| `/chatshop names` | — | Browse name colors | `lpcpro.shop` |
| `/chatshop tags` | — | Browse tags | `lpcpro.shop` |
| `/chatshop perks` | — | Browse perks | `lpcpro.shop` |
| `/chatshop give <player> <amount>` | `add` subcommand | Credit an online player's active shop balance | `lpcpro.shop.admin` |
| `/chatshop set <player> <amount>` | — | Set an online player's active shop balance | `lpcpro.shop.admin` |
| `/chatshop take <player> <amount>` | `remove` subcommand | Debit an online player's active shop balance | `lpcpro.shop.admin` |
| `/chatshop recover <player> <item-id> <paid\|not-paid>` | — | Reconcile an uncertain Vault payment after checking its ledger | `lpcpro.shop.admin` |

These are in-game commands. Administrative subcommands also require the base `lpcpro.shop` access. `give` and `take` use positive whole amounts; `set` allows zero. They change internal points in points mode and the connected economy balance in Vault mode.

## Currency Modes

The shop supports two currency backends:

```yaml
currency-mode: "points"
currency-name: "Points"
```

| Mode | Description |
|---|---|
| `points` | Internal LPC Pro points; the default |
| `vault` | The connected Vault economy provider; requires Vault and an economy plugin |

Item currency is not implemented. In Vault mode, an unavailable or rejecting provider cannot complete a purchase, and LPC does not switch to points silently.

### Earning Points

These are the default earning values, read from the `earning:` section:

```yaml
earning:
  chat:
    enabled: true
    points-per-message: 1
    cooldown-seconds: 15
  playtime:
    enabled: true
    points-per-hour: 10
  games:
    enabled: true
    points-per-win: 5
```

Earning uses the active currency mode: internal points in points mode and deposits through the provider in Vault mode. Review these values when switching to Vault so normal chat or playtime rewards fit your economy. Set the relevant option to `false` to disable a source.

## Configuration

```yaml
pagination:
  items-per-page: 21
```

`items-per-page` is limited to 1–21. Use `14` for two rows per page or `7` for one row. Categories with more items gain navigation arrows.

### Shop Items

On a fresh setup, an empty item catalog is populated with the built-in offers. Edit the resulting `items:` map to customize them. This example shows one color and two supported perks; merge entries into your existing map rather than replacing the entire catalog:

```yaml
items:
  color_red:
    name: "Red Chat Color"
    category: "CHAT_COLOR"
    material: "RED_DYE"
    price: 100
    value: "<red>"
    permission: "lpcpro.color.red"
    enabled: true
  perk_extra_qr:
    name: "Extra Quick Replies (+5)"
    category: "PERK"
    material: "BOOK"
    price: 400
    value: "5"
    permission: "lpcpro.quickreply.extra"
    perk-kind: "QUICK_REPLY_SLOTS"
    enabled: true
  perk_no_cooldown:
    name: "Reduced Cooldown"
    category: "PERK"
    material: "CLOCK"
    price: 600
    value: "reduced"
    permission: "lpcpro.bypass.cooldown.partial"
    perk-kind: "REDUCED_NORMAL_CHAT_COOLDOWN"
    enabled: true
```

Categories are `CHAT_COLOR`, `NAME_COLOR`, `TAG` and `PERK`. Prices are nonnegative whole numbers. `custom-model-data` is optional and controls the item's resource-pack appearance. Keep item IDs stable so existing ownership continues to match.

Cosmetic access can come from an existing permission or a confirmed purchase. Buying an item does not grant a permanent permission node in LuckPerms. Selected cosmetics are stored in player settings and can be saved in [player style profiles](player-style-profiles.md).

### Supported Perks

| `perk-kind` | Value | Effect |
|---|---|---|
| `QUICK_REPLY_SLOTS` | Whole number from `1` to `1000` | Adds slots to the base quick-reply limit; highest accessible bonus applies once |
| `REDUCED_NORMAL_CHAT_COOLDOWN` | `"reduced"` | Halves normal anti-spam delay, rounded up, minimum one second |

For example, base 5 plus a purchased bonus of 5 gives 10 quick replies. A larger manually granted rank limit of 15 remains 15. Bonuses do not stack.

Reduced cooldown affects only the normal anti-spam timer. Global, raid, channel and newcomer slowmode floors still apply, as do mute, anti-bot and similarity checks. It does not turn cooldowns off entirely.

Unsupported perks, including the old 512-character message offer, are unavailable for purchase. Existing ownership is retained, with no automatic refund or deletion. A disabled perk remains visible as unavailable and grants no effect. Upgrades that give no additional benefit cannot charge a player.

After editing, use `/lpc reload`, reopen the shop and check the available offers. An already open menu belongs to the previous catalog and may require reopening.

## Payment Recovery

When a Vault provider's result is uncertain, LPC retains a record in `lpcpro_shop_journal`. Staff must check the external economy ledger before choosing a result:

```text
/chatshop recover Steve perk_extra_qr paid
```

Use `paid` only when the withdrawal was confirmed; use `not-paid` only when it was not charged. This reconciles a record; it is not a new payment or refund command. Preserve database backups while investigating.

## Permissions

| Permission | Description |
|---|---|
| `lpcpro.shop` | Access the shop and player commands |
| `lpcpro.shop.admin` | Manage the active currency balance and reconcile uncertain payments |

## PlaceholderAPI

| Placeholder | Description |
|---|---|
| `%lpcpro_balance%` | LPC's balance placeholder for an online player |
| `%lpcpro_balance_formatted%` | Compact balance display, such as `1.2K` |

For the active provider's exact displayed balance, use `/chatshop balance`.
