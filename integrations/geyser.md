# 🌉 Geyser & Floodgate

LPC Pro can use a connected Geyser or Floodgate provider to show native Bedrock forms for recent chat actions and personal settings. Floodgate is not required when Geyser-Spigot exposes the player's real connection.

## Setup

1. Configure a working Geyser connection for your server. Install Floodgate only if your chosen authentication/setup needs it.
2. Keep the following main setting enabled:

```yaml
hooks:
  geyser: true
```

3. Join from Bedrock and try `/chatmenu` and `/toggle menu`.

The form API must be available on the backend running LPC Pro. A proxy-only installation that does not expose the connection there cannot be assumed to provide forms. A name prefix or UUID pattern alone is not enough to authorize these menus.

## Recent Chat Actions

`/chatmenu` requires `lpcpro.chatmenu` (default: `true`). It lists up to five local messages actually delivered to the current connection, with a default lifetime of 120 seconds. Text is bounded to 256 characters.

Available actions depend on the source and the player's current permissions:

- Open a delivered inventory, ender chest, or held-shulker snapshot.
- Write a public reply when public replies are enabled and available.
- Start a private reply, ignore the source player, or report the captured context.

The source must still be valid and the player must still have channel access. Quit/rejoin, source logout, reload, and source deletion can invalidate actions. This is a local recent-message menu, not a searchable cross-server chat archive.

The setting is in `advanced/variables.yml`:

```yaml
bedrock-actions:
  enabled: true
```

This is an excerpt; preserve the other variable settings.

## Personal Settings

`/toggle menu` opens a native settings form for a connected Bedrock player. It offers the available public chat, game, PM, DND, mention, sound, join/quit/death, and mention-tone choices. Saved choices persist between sessions.

The normal command alternatives remain available. `/toggle gui` opens the Java inventory for mention sounds; it is not another name for the native settings form.

## Inventory Previews

Snapshot actions open read-only inventories through Geyser. Items cannot be taken from the preview. These inventories are not all converted into native forms: provider translation can add blocked padding slots and shorten long titles. Public replies and inventory/shulker viewers are unavailable on Folia.

## Provider Information

Floodgate can also expose a Bedrock gamertag and device information where its API supports them. This metadata path is separate from genuine connection checking for forms. A working Geyser-only form connection does not imply every Floodgate metadata value is available.

The device checks covered Bedrock 26.52 through Geyser. They do not establish compatibility with every newer Bedrock transport or provider build. Follow Geyser's current connection requirements when upgrading your clients/provider.
