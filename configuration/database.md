# Database

LPC Pro stores player data, mutes, warnings, reputation, chat logs, and more in a database. Configuration is in `database.yml`.

## SQLite (Default)

SQLite requires zero configuration. Data is stored in a local `lpcpro.db` file inside the plugin folder.

```yaml
type: local
```

This is the recommended option for single servers.

## MySQL / MariaDB

For larger servers or BungeeCord/Velocity networks, use a remote MySQL/MariaDB database:

```yaml
type: remote

host: localhost:3306
database: lpcpro
username: your_username
password: your_password
```

### Requirements

- **MySQL 8.0+** or **MariaDB 10.3+**
- Collation: `utf8mb4_unicode_520_ci` (required for emoji and unicode support)

### Creating the Database

```sql
CREATE DATABASE lpcpro
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_unicode_520_ci;
```

LPC Pro will automatically create all required tables on startup.

## Connection String

For advanced users, you can customize the JDBC connection string:

```
jdbc:{driver}://{host}/{database}?autoReconnect=true&characterEncoding=UTF-8&tcpKeepAlive=true&useSSL=false
```

LPC Pro uses **HikariCP** for connection pooling, which handles reconnection automatically.

{% hint style="danger" %}
`database.yml` does **not** support reloading. Any changes require a full server restart.
{% endhint %}

## Data Stored

The following data is persisted in the database:

| Table | Purpose |
|---|---|
| `lpcpro_channels` | Custom chat channel definitions |
| `lpcpro_player_channels` | Channel membership and modes |
| `lpcpro_ignored_players` | Player ignore lists |
| `lpcpro_mutes` | Active and expired mutes |
| `lpcpro_warnings` | Player warnings |
| `lpcpro_player_notes` | Staff notes on players |
| `lpcpro_reputation` | Reputation scores |
| `lpcpro_reputation_log` | Reputation transaction log |
| `lpcpro_reports` | Chat reports |
| `lpcpro_polls` | Poll data |
| `lpcpro_poll_votes` | Poll vote records |
| `lpcpro_offline_messages` | Messages for offline players |
| `lpcpro_player_settings` | Per-player settings (color, toggles) |
| `lpcpro_chat_logs` | Chat message log |
| `lpcpro_chat_stats` | Player chat statistics (message counts, mentions, replies) |
| `lpcpro_achievements` | Unlocked achievements per player |
| `lpcpro_quick_replies` | Saved quick reply messages |
| `lpcpro_newcomer` | Newcomer tracking (playtime, message count) |
| `lpcpro_shop_purchases` | Shop item purchase records |
| `lpcpro_shop_points` | Player shop currency balances |
| `lpcpro_mail` | Mail messages between players |
| `lpcpro_player_language` | Player language preferences for translation |
