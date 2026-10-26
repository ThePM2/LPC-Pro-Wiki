# 🗄️ Database

LPC Pro stores channels, settings, mutes, warnings, reputation, chat logs, purchases, and other records in a database. Connection settings are in the root `database.yml`.

## SQLite (Default)

SQLite needs no connection configuration. Data is stored in `plugins/LPC-Pro/lpcpro.db`:

```yaml
type: local
```

This is the simplest starting point for a single server. LPC uses SQLite's WAL mode. Stop the server cleanly before taking a file backup; copying only the main database while it is being written may miss pending WAL data.

## MySQL / MariaDB

The remote path uses MySQL Connector/J. Configure the host and port as separate fields:

```yaml
type: remote
host: 127.0.0.1
port: 3306
database: lpcpro
username: lpcpro
password: 'replace-with-your-database-password'
```

Use a dedicated account with the permissions needed to create/alter LPC tables and read/write its data. MySQL 8 is the intended remote target. MariaDB compatibility depends on the installed server and driver combination; it has not been established for every version.

### Creating the Database

Use a database supporting four-byte Unicode for chat, emoji, and non-English names:

```sql
CREATE DATABASE lpcpro
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_unicode_520_ci;
```

This is an example compatible collation; create users/grants separately according to your database host. LPC creates and migrates its required tables on startup. Required schema failures prevent normal plugin startup rather than silently reporting an empty store.

## Connection Settings

LPC uses HikariCP pooling. The current remote URL uses MySQL's `sslMode=PREFERRED`; this is opportunistic encryption, not a promise of certificate-verified TLS. There is no configurable custom JDBC `line` or driver field in `database.yml`.

{% hint style="danger" %}
Database settings require a full server restart. Changing `type` selects another store; it does not automatically transfer SQLite data to MySQL or migrate existing balances between them.
{% endhint %}

## Data Stored

| Table / State | Purpose |
|---|---|
| `lpcpro_channels`, `lpcpro_player_channels` | Stored channel definitions, membership, and write selection |
| `lpcpro_channel_focus` | Personal automatic/manual channel focus |
| `lpcpro_ignored_players` | Ignore lists |
| `lpcpro_mutes`, `lpcpro_warnings`, `lpcpro_player_notes` | Staff moderation records |
| `lpcpro_reputation`, `lpcpro_reputation_log` | Reputation and its transaction log |
| `lpcpro_reports` | Player reports |
| `lpcpro_polls`, `lpcpro_poll_votes` | Polls and votes |
| `lpcpro_offline_messages`, `lpcpro_mail` | Offline messages and mail |
| `lpcpro_player_settings` | Cosmetics, toggles, and receiving preferences |
| `lpcpro_newcomer` | Persistent newcomer progress |
| `lpcpro_quick_replies` | Saved personal quick replies |
| `lpcpro_chat_profiles`, `lpcpro_chat_profile_owners` | Saved personal style profiles |
| `lpcpro_chat_logs`, `lpcpro_chat_stats` | Chat history and statistics |
| `lpcpro_achievements`, `lpcpro_achievement_mentions` | Achievement progress |
| `lpcpro_shop_purchases`, `lpcpro_shop_points` | Internal points and shop ownership |
| `lpcpro_player_language` | Translation preferences |
| `lpcpro_schema_version` | Completed ordered schema migrations |

Additional feature-owned records cover purchases/rewards and recovery. Not all state is SQL: for example, automatic infractions use `data/infractions.json`, and review/cache files have separate lifetimes. Back up the entire LPC-Pro directory as well as a remote database.

## Health and Recovery

`/lpc status` shows schema health and pending/failed/rejected storage work. Accepted writes are queued and drained on normal shutdown; a forced kill or power loss can still interrupt work. If settings storage fails, a player may need to reconnect after repair to reload durable values.

A shared remote database is not a distributed cache-invalidation system. Online settings are session snapshots; simultaneous sessions on different backends should not be treated as strongly consistent. Configure the [authenticated proxy relay](../integrations/proxy.md) for supported live notifications.
