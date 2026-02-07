# 🔇 Muting

LPC Pro supports three types of mutes: player mutes, channel mutes, and server-wide mutes. All mutes support optional durations and are persisted in the database.

## Commands

### Mute Command

The `/mute` command handles all mute types through subcommands:

| Command | Description | Permission |
|---|---|---|
| `/mute <player> [duration] [reason]` | Mute a player (shorthand) | `lpcpro.mute` |
| `/mute player <player> [duration] [reason]` | Mute a player | `lpcpro.mute` |
| `/mute channel <channel> [duration] [reason]` | Mute a chat channel | `lpcpro.mute.channel` |
| `/mute server [duration] [reason]` | Mute all server chat | `lpcpro.mute.server` |

### Unmute Command

The `/unmute` command mirrors the same structure:

| Command | Description | Permission |
|---|---|---|
| `/unmute <player>` | Unmute a player (shorthand) | `lpcpro.mute` |
| `/unmute player <player>` | Unmute a player | `lpcpro.mute` |
| `/unmute channel <channel>` | Unmute a channel | `lpcpro.mute.channel` |
| `/unmute server` | Unmute server chat | `lpcpro.mute.server` |

### View Mutes

| Command | Description | Permission |
|---|---|---|
| `/mutes <player>` | View a player's mute history | `lpcpro.mute.view` |

## Duration Format

Durations use a shorthand format:

| Suffix | Unit | Example |
|---|---|---|
| `s` | Seconds | `30s` |
| `m` | Minutes | `15m` |
| `h` | Hours | `2h` |
| `d` | Days | `7d` |
| `w` | Weeks | `2w` |
| `perm` | Permanent | `perm` |

Omitting the duration creates a permanent mute.

## Examples

```
/mute Steve 30m Spamming in chat
/mute Steve                        # Permanent mute, no reason
/mute channel global 1h            # Mute global channel for 1 hour
/mute server 15m                   # Mute all chat for 15 minutes
/unmute Steve                      # Unmute a player
/unmute channel global             # Unmute a channel
/unmute server                     # Unmute server chat
```

## Mute Types

### Player Mute

Prevents a specific player from sending chat messages. Muted players can still use commands.

### Channel Mute

Prevents all non-bypassing players from chatting in a specific channel. Useful for locking a channel during events or maintenance.

### Server Mute

Prevents all non-bypassing players from chatting anywhere on the server.

## Bypass

| Permission | Default | Description |
|---|---|---|
| `lpcpro.bypass.mute` | `op` | Chat even when muted |

{% hint style="warning" %}
The `bypass-mute` group property in `advanced/groups.yml` is loaded from config but is **not currently checked** by the mute system. Use the `lpcpro.bypass.mute` permission to allow staff to chat through mutes.
{% endhint %}

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.mute` | `op` | Mute/unmute players |
| `lpcpro.mute.channel` | `op` | Mute/unmute channels |
| `lpcpro.mute.server` | `op` | Mute/unmute the server |
| `lpcpro.mute.view` | `op` | View mute history |
| `lpcpro.bypass.mute` | `op` | Bypass mute restrictions |
