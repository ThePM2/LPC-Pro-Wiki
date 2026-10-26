# ✉️ Private Messages

LPC Pro provides a full private messaging system with customizable formats, ignore lists, and staff spy functionality.

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/msg <player> <message>` | `/m`, `/tell`, `/t`, `/whisper`, `/w` | Send a private message | `lpcpro.command.msg` |
| `/r <message>` | `/reply` | Reply to last message | `lpcpro.command.reply` |
| `/ignore <player>` | — | Ignore a player's messages | `lpcpro.command.ignore` |
| `/unignore <player>` | — | Stop ignoring a player | `lpcpro.command.unignore` |

## Enabling / Disabling

Private messages are controlled in `config.yml`:

```yaml
enable-private-messages: true
enable-ignore-messages: true
```

{% hint style="warning" %}
Changing these settings requires a **server restart** because the commands are registered dynamically on startup.
{% endhint %}

When `enable-private-messages` is `true`, ignore messages are automatically enabled regardless of the `enable-ignore-messages` setting.

## Message Formats

Private message formats are defined in separate format files:

- **Sender sees:** `formats/msg-sender.yml`
- **Receiver sees:** `formats/msg-receiver.yml`

### Sender Format Example

```yaml
msg:
  text: "<#6cc324>[&fme <#6cc324>➥ &f{receiver_name}<#6cc324>] &f{message}"
  hover:
    - "&8%server_time_yyyy-MM-dd HH:mm:ss%"
    - "You <#6cc324>sent this message to &f{receiver_name}<#6cc324>."
    - ""
    - "<#6cc324>Click to reply!"
  suggest: "/msg {receiver_name} "
```

### Receiver Format Example

```yaml
from-to:
  text: "<#6cc324>[&f{sender_name} <#6cc324>➥ &fme<#6cc324>]"
  hover:
    - "&8%server_time_yyyy-MM-dd HH:mm:ss%"
    - "{sender_name} <#6cc324>sent this message to &fyou<#6cc324>."
    - ""
    - "<#6cc324>Click to reply!"
  suggest: "/msg {sender_name} "

message:
  text: "{message}"
  hover: "&eClick to report {sender_name}'s message!"
  suggest: "/report {sender_name} "
```

### Available Placeholders

| Placeholder | File | Description |
|---|---|---|
| `{receiver_name}` | msg-sender.yml | The recipient's name |
| `{sender_name}` | msg-receiver.yml | The sender's name |
| `{message}` | Both | The message content |

## Ignore System

Players can ignore other players to stop receiving their messages:

- `/ignore <player>` — Block messages from a player
- `/unignore <player>` — Unblock a player

Ignore lists are persisted in the database and survive server restarts.

### Ignore Bypass

`lpcpro.command.ignore.bypass` prevents players from newly ignoring that target while the target is online and the permission can be checked. It does not override an already saved ignore at delivery time, and it does not bypass the recipient's PM or DND preference.

## Staff Spy

Staff members can spy on private messages:

| Permission | Description |
|---|---|
| `lpcpro.spy.pm` | Access `/spy` to enable private-message spy |
| `lpcpro.spy.bypass` | Your messages won't be seen by spies |

## Do Not Disturb

Players can toggle Do Not Disturb mode to temporarily stop receiving private messages:

| Command | Permission | Description |
|---|---|---|
| `/dnd` | `lpcpro.dnd` | Toggle Do Not Disturb mode |
| `/dnd on` / `/dnd off` | `lpcpro.dnd` | Set DND explicitly |
| `/dnd message <message>` | `lpcpro.dnd` | Save your DND auto-reply |

`/toggle pm` controls PM receiving separately. PMs are on and DND is off by default. Preferences and the DND auto-reply are saved. If recipient settings or ignore data are still loading, LPC Pro asks the sender to try again rather than delivering without those checks.

## Moderation

Private messages are subject to the swear filter when `filter-private-messages: true` is set in `moderation/moderation.yml`.


## Offline Players and Other Chat Plugins

`/msg Steve Hello!` uses the real account name, not a cosmetic nickname. If Steve is offline and the [Offline Messages](offline-messages.md) feature is enabled, the message can be queued for the next eligible login. A vanished player is not exposed to a sender without vanish access.

If another plugin owns `/msg`, check `override-conflicting-commands` in `config.yml`. LPC Pro's default takeover list includes PM, reply, ignore and mail labels; other plugins' namespaced commands stay available. You can also address LPC Pro's command through `/lpcpro:msg` when it is registered.

Ignore lists affect both private and local channel delivery. Saving an ignore is acknowledged only when its database update succeeds. Staff spy must be switched on with `/spy`; possession of the permission alone is not a claim that a message was displayed to a staff client.
