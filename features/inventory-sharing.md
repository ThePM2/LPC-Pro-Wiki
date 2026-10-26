# 🎒 Inventory & Shulker Sharing

Players can share a frozen view of their inventory or ender chest in local channel chat. Recipients click the delivered label to open a **read-only snapshot**. Taking, moving or dropping items from this view is blocked.

## Usage

| Token | What is shared |
|---|---|
| `[item]` | The item held when the message is prepared, with its normal tooltip |
| `[inv]` | Main inventory, armor and offhand snapshot |
| `[ender]` | Personal ender chest snapshot |

For example, type these as chat messages:

```text
Selling this [item]
Here is my mining loadout: [inv]
Spare supplies are in [ender]
```

The view shows the captured state, not a live inventory. Later item changes do not update an existing snapshot. Inventory sharing captures 36 storage slots, four armor slots and the offhand; ender sharing captures 27 slots.

`[inv]` and `[ender]` are supported in the local channel pipeline, not as portable links in private messages, mail or a proxy relay. The internal `/lpcview <token>` command opens a delivered snapshot; players normally use the chat label instead of typing it.

## Shulker Contents

When `[item]` shares a held shulker box, its delivered item label can open the captured contents. In an `[inv]` or `[ender]` view, left-click a shulker to inspect one layer of contents. **Back** returns to the correct parent view; the held-item shulker view has **Close** instead.

Only one shulker layer is opened. Shulkers inside that view do not create a recursive browser. There is no separate `[shulker]` chat token.

The normal server-side shulker view has 27 content slots and a navigation row. Geyser may display extra blocked padding slots and clip longer titles; those slots are not shared storage.

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.variable.item` | Not declared in `plugin.yml` | Use the existing `[item]` feature, including a held shulker; grant it explicitly to intended players |
| `lpcpro.variable.inv` | `true` | Share `[inv]` |
| `lpcpro.variable.ender` | `true` | Share `[ender]` |
| `lpcpro.variable.inv.view` | `true` | View a delivered inventory snapshot |
| `lpcpro.variable.ender.view` | `true` | View a delivered ender snapshot |
| `lpcpro.variable.shulker.view` | `true` | Open shulker contents |

Opening a shulker inside an inventory or ender view still requires access to its parent snapshot. A permission does not allow viewing snapshots that were never delivered to that connection.

## Configuration

The live file is `plugins/LPC-Pro/advanced/variables.yml`. These are the inventory-sharing defaults:

```yaml
inventory-sharing:
  enabled: true
  ttl-seconds: 300
  max-per-player: 4
  max-global: 128
  max-viewers: 256
  cooldown-seconds: 10
  max-tokens-per-message: 4
  max-bytes-per-item: 65536
  max-bytes-per-snapshot: 262144
  shulker-preview-enabled: true
```

| Setting | Allowed values | Description |
|---|---|---|
| `ttl-seconds` | `1`–`300` | Snapshot lifetime |
| `max-per-player` | `1`–`4` | Captures retained for one owner |
| `max-global` | `1`–`128` | Captures retained on this backend |
| `max-viewers` | `1`–`256` | Recipient grants per snapshot |
| `cooldown-seconds` | `0`–`60` | Minimum time between accepted captures |
| `max-tokens-per-message` | `1`–`4` | Maximum visible share tokens |
| `max-bytes-per-item` | `1`–`65536` | Serialized item size limit |
| `max-bytes-per-snapshot` | `1`–`262144` | Combined serialized size limit |

The existing item-display section is separate:

```yaml
item-variable:
  enabled: true
  display-format: "<aqua>[<item_name>]</aqua>"
  max-uses-per-message: 3
```

`<item_name>` and `<amount>` are special item-display replacements. Disabling `shulker-preview-enabled` removes content previews while retaining ordinary item tooltips. Use `/lpc reload` after changes.

## Access & Expiry

Recipients must have received the message in their current connection and still have channel access and view permission. Ignoring the owner prevents access. Links cannot be transferred to another player or reused after reconnecting.

Snapshots are temporary memory, not saved inventory backups. They expire after the configured lifetime. Owner death, disconnect or a reload invalidates the corresponding views. Empty the cursor before opening; a held cursor item causes the viewer to refuse opening.

If a cooldown, capacity or size limit prevents a capture, the token may remain ordinary text with a notice. Do not increase limits beyond the supported ranges; wait for expiry or send a new snapshot later.

## Bedrock & Folia

Connected Bedrock players can find delivered inventory actions through `/chatmenu`; the snapshot itself opens as a read-only inventory. See [Bedrock Support](../integrations/geyser.md) for provider requirements.

Inventory, ender and shulker snapshot viewers are unavailable on Folia in this version. Existing ordinary `[item]` tooltip behavior remains separate.
