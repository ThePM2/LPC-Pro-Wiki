# 📋 Requirements

Before installing LPC Pro, choose a server build and Java version that work together.

## Server Requirements

| Requirement | Details |
|---|---|
| **Server Software** | Paper is recommended. Spigot uses the plugin's Adventure compatibility layer. Folia has the limits below. |
| **Plugin Version** | This documentation describes 2.6.0. |
| **Java Version** | Use the Java version required by your server build. The plugin targets Java 16 bytecode; this is not the Java requirement of modern Minecraft servers. |

[Paper's Java recommendations](https://docs.papermc.io/paper/getting-started/#requirements) list Java 17 for 1.17–1.19, Java 21 for 1.20–1.21.11, and Java 25 for 26.1+. Follow your server's own requirements when using another implementation.

{% hint style="info" %}
**Paper is recommended** for native Adventure support. Install and try the plugin on a copy of your server before upgrading your live server, especially when changing Minecraft versions or chat integrations.
{% endhint %}

## Checked Compatibility

The 2.6.0 release was checked on Paper 1.21.5 with Java 21 for fresh startup, an existing-data upgrade, reload, and connected-client chat and inventory delivery. Its plugin class files are identical to the candidate used for Java 26.3 and Bedrock 26.52 device checks. The existing-data check used a private test server; it was not an upgrade from every published LPC Pro binary.

A Java 26.3 client joining through ViaVersion is a **client compatibility** check, not a native 26.3 server check. Bedrock 26.60/NetherNet, every historical server release, arbitrary modded servers, and real-provider AI classification quality were not certified by these release checks.

## Folia Limits

Folia support does not enable every feature. Range/world-limited channels, chat bubbles, managed deletion/replay, ProtocolLib interception, `@here`, inventory/ender/shulker viewers, and public replies are unavailable. Relational PlaceholderAPI placeholders are unavailable in the shared rendering path. Some teleport operations are also disabled.

Configured console/reward commands are blocked on Folia by default. Only enable `folia.allow-unsafe-console-commands` after checking that every configured command supports Folia. Check `/lpc status` and the startup log for feature availability.

## Optional Dependencies

| Plugin | What It Enables |
|---|---|
| [LuckPerms](https://luckperms.net/) | Rank metadata and primary-group formatting |
| [Vault](https://github.com/MilkBowl/Vault) | Permission/chat integration and a bridge to a separately installed economy provider |
| [PlaceholderAPI](https://github.com/PlaceholderAPI/PlaceholderAPI/wiki) | External `%placeholder%` expansions |
| [ProtocolLib](https://github.com/dmulloy2/ProtocolLib) | Optional interception of supported outgoing messages; LPC-managed deletion has its own settings |
| [DiscordSRV](https://docs.discordsrv.com/) | Optional incoming Discord messages; outgoing webhooks are configured separately |
| [ItemsAdder](https://itemsadder.devs.beer/), [Oraxen](https://docs.oraxen.com/), [Nexo](https://docs.nexomc.com/) | Their own custom font/glyph integrations |
| [Geyser](https://geysermc.org/) / [Floodgate](https://geysermc.org/wiki/floodgate/) | Genuine Bedrock connection detection and optional native forms; Floodgate is not required for a supported Geyser connection |
| [ViaVersion](https://viaversion.com/) | Optional client version detection and compatible cross-version connections |
| EssentialsX, SuperVanish, PremiumVanish | Vanish awareness through the supported hooks/metadata |

No optional hook installs or configures its provider for you. Provider versions, fonts, permissions, and server support must also be compatible. See the individual [integration guides](../integrations/luckperms.md).

## Database

SQLite is the default local backend. MySQL can be configured in `database.yml`; use a backed-up database and a user with the permissions needed for schema migrations. Sharing a database does not automatically synchronize every online cache or replace authenticated proxy transport. See [Database](../configuration/database.md).
