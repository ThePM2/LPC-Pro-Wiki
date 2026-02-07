# Discord Integration

LPC Pro can bridge chat between your Minecraft server and Discord channels using webhooks and/or DiscordSRV. Configuration is in `integration/discord.yml`.

## Setup

### Step 1: Enable the Integration

```yaml
enabled: true
```

### Step 2: Create a Discord Webhook

1. Open your Discord server settings
2. Go to **Integrations** > **Webhooks**
3. Click **New Webhook**
4. Choose the channel where Minecraft messages should appear
5. Copy the webhook URL

### Step 3: Configure Channel Mapping

Map your LPC Pro channels to Discord channels:

```yaml
channels:
  global:
    webhook-url: "https://discord.com/api/webhooks/YOUR_ID/YOUR_TOKEN"
    discord-channel-id: "YOUR_CHANNEL_ID"
    send-to-discord: true
    receive-from-discord: true
    format-to-discord: "{player}: {message}"
    format-from-discord: "<blue>[Discord]</blue> <white>{username}</white>: <gray>{message}</gray>"
```

## Configuration Reference

```yaml
enabled: false
use-discordsrv: true           # Use DiscordSRV for receiving messages
bot-name: "LPC Pro"            # Bot display name for webhooks
avatar-url: ""                 # Bot avatar URL for webhooks

channels:
  global:
    webhook-url: "https://discord.com/api/webhooks/..."
    discord-channel-id: "123456789"
    send-to-discord: true       # Send MC messages to Discord
    receive-from-discord: true  # Receive Discord messages in MC
    format-to-discord: "{player}: {message}"
    format-from-discord: "<blue>[Discord]</blue> <white>{username}</white>: <gray>{message}</gray>"
```

### Settings

| Setting | Type | Description |
|---|---|---|
| `webhook-url` | string | Discord webhook URL for sending messages |
| `discord-channel-id` | string | Discord channel ID (for receiving via DiscordSRV) |
| `send-to-discord` | boolean | Forward Minecraft messages to Discord |
| `receive-from-discord` | boolean | Forward Discord messages to Minecraft |
| `format-to-discord` | string | Message format sent to Discord |
| `format-from-discord` | string | Message format shown in Minecraft (MiniMessage) |

### Placeholders

**To Discord:** `{player}`, `{message}`

**From Discord:** `{username}`, `{message}`

## DiscordSRV

If you have [DiscordSRV](https://www.spigotmc.org/resources/discordsrv.18494/) installed, LPC Pro can use it to receive messages from Discord. Set `use-discordsrv: true` and configure the `discord-channel-id` for each channel mapping.

Without DiscordSRV, only sending to Discord (via webhooks) is supported.

## Multiple Channels

You can map multiple LPC Pro channels to different Discord channels:

```yaml
channels:
  global:
    webhook-url: "https://discord.com/api/webhooks/global-webhook..."
    discord-channel-id: "111111111"
    send-to-discord: true
    receive-from-discord: true

  staff:
    webhook-url: "https://discord.com/api/webhooks/staff-webhook..."
    discord-channel-id: "222222222"
    send-to-discord: true
    receive-from-discord: true
```
