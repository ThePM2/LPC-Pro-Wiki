# 📬 Mail System

The mail system allows players to send messages to offline players. When the recipient logs in, they receive a notification with their unread mail. Configuration is in `features/mail.yml`.

## Commands

| Command | Description |
|---|---|
| `/mail` | View your inbox |
| `/mail send <player> <message>` | Send mail to a player (online or offline) |
| `/mail read <id>` | Read a specific mail message |
| `/mail reply <id> <message>` | Reply to a mail message |
| `/mail delete <id>` | Delete a specific mail message |
| `/mail clear` | Clear all mail |
| `/mail page <number>` | Open another inbox page |

**Alias:** `/email`

**Permission:** `lpcpro.mail`

## Configuration

```yaml
enabled: true
permission: "lpcpro.mail"

mail:
  max-inbox-size: 50        # Maximum mails per player
  max-message-length: 500   # Maximum characters per mail
  expiration-days: 30        # Days before mail expires (0 = never)
  allow-self-mail: false     # Allow mailing yourself

notifications:
  notify-on-login: true      # Notify on login if unread mail exists
  login-notify-delay: 60     # Delay in ticks (60 = 3 seconds)
  notification-sound: "ENTITY_EXPERIENCE_ORB_PICKUP"
  sound-volume: 1.0
  sound-pitch: 1.0
```

## Settings Reference

| Setting | Type | Default | Description |
|---|---|---|---|
| `max-inbox-size` | integer | `50` | Maximum number of mails in a player's inbox |
| `max-message-length` | integer | `500` | Maximum characters per mail message |
| `expiration-days` | integer | `30` | Days before mail expires, whether read or unread (`0` = never) |
| `allow-self-mail` | boolean | `false` | Whether players can send mail to themselves |
| `notify-on-login` | boolean | `true` | Notify players about unread mail when they join |
| `login-notify-delay` | integer | `60` | Ticks to wait before showing the notification |


## Sending and Saving Mail

Both `enable-mail` in `config.yml` and `enabled` in this file must be on. Grant the configured `permission` to players who should use mail; `lpcpro.mail` is not explicitly granted to all players in the plugin descriptor. A change to `enable-mail` needs a restart; other mail settings use `/lpc reload`.

```text
/mail send Steve Your building materials are ready at spawn.
/mail
/mail read 12
/mail reply 12 Thank you!
```

Use an ID from your own inbox. Only the recipient can read or delete a mail entry. Mail can be sent to known players who have joined before, whether currently online or offline. Mail from the server cannot be replied to. Inbox pages show eight entries each.

Mail is stored separately from the automatic [Offline Messages](offline-messages.md) queue. A send is acknowledged after storage completes; if the inbox is full or storage fails, it is not reported as sent. Expiry applies to read and unread messages. Saved mail does not become a live private conversation or use the recipient's chat format.
