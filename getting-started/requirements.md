# Requirements

Before installing LPC Pro v2, make sure your server meets the following requirements.

## Server Requirements

| Requirement | Details |
|---|---|
| **Server Software** | Paper (recommended) or Spigot |
| **Minecraft Version** | 1.17 - 1.21.11 |
| **Java Version** | Java 16 or higher (Java 17+ recommended for Paper 1.18+) |

{% hint style="info" %}
**Paper is strongly recommended** over Spigot. LPC Pro uses the Adventure API for rich text formatting (MiniMessage, hex colors, gradients, click actions, hover tooltips). Paper includes Adventure natively, while Spigot requires a compatibility layer.
{% endhint %}

## Optional Dependencies

These plugins are **not required** but enable additional features when installed:

| Plugin | What It Enables |
|---|---|
| [LuckPerms](https://luckperms.net/) | Group detection, prefix/suffix in chat formats |
| [Vault](https://www.spigotmc.org/resources/vault.34315/) | Economy integration, permission abstraction |
| [PlaceholderAPI](https://www.spigotmc.org/resources/placeholderapi.6245/) | `%placeholder%` support in chat formats and hover text |
| [ProtocolLib](https://www.spigotmc.org/resources/protocollib.1997/) | Message deletion (the clickable `[X]` button), message interception |
| [DiscordSRV](https://www.spigotmc.org/resources/discordsrv.18494/) | Receiving Discord messages in Minecraft |
| [ItemsAdder](https://www.spigotmc.org/resources/itemsadder.73355/) | Custom emoji support (`:emoji:` syntax) |
| [Oraxen](https://www.spigotmc.org/resources/oraxen.72448/) | Custom glyph support (`:glyph:` syntax) |
| [Geyser](https://geysermc.org/) + [Floodgate](https://wiki.geysermc.org/floodgate/) | Bedrock player detection |
| [ViaVersion](https://www.spigotmc.org/resources/viaversion.19254/) | Client version detection |
| [Essentials](https://essentialsx.net/) | Vanish detection via Bukkit metadata |
| [SuperVanish](https://www.spigotmc.org/resources/supervanish.1331/) / [PremiumVanish](https://www.spigotmc.org/resources/premiumvanish.14404/) | Vanished player awareness in chat, mentions, and tab completion |

## Database

LPC Pro supports two database backends:

- **SQLite** (default) — Zero configuration, works out of the box. Stored as a local `lpcpro.db` file in the plugin folder.
- **MySQL / MariaDB** — Recommended for larger servers or BungeeCord/Velocity networks. Requires MySQL 8.0+ with `utf8mb4_unicode_520_ci` collation for full emoji and unicode support.
