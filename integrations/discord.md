# 💜 Discord Integration

LPC Pro can relay chat between Minecraft and Discord using webhooks and/or DiscordSRV. Configuration is in `integration/discord.yml`.

## Setup

### Step 1: Enable the Integration

Keep `enable-discord: true` in the main `config.yml` and set `enabled: true` in `integration/discord.yml`. The main switch requires a restart if changed; the integration file supports `/lpc reload`.

### Step 2: Choose a Relay Mode

| `relay-mode` | Minecraft to Discord |
|---|---|
| `auto` | Use a valid channel webhook; otherwise use the configured DiscordSRV destination when its lookup API is available |
| `webhook` | Use the configured channel webhook |
| `discordsrv` | Let DiscordSRV handle delivery and its own formatting/avatar pipeline |

The default is `auto`. Webhooks use the configured single bot name/avatar, rather than automatically giving each player a separate avatar.

### Step 3: Configure Channel Mapping

For webhook delivery, create a webhook for your Discord channel and copy its URL into the matching LPC channel. Keep its token private.

```yaml
enabled: true
use-discordsrv: true
relay-mode: "auto"
bot-name: "LPC Pro"
avatar-url: ""

channels:
  global:
    webhook-url: "https://discord.com/api/webhooks/YOUR_WEBHOOK_ID/YOUR_WEBHOOK_TOKEN"
    discord-channel-id: "YOUR_DISCORD_CHANNEL_ID"
    send-to-discord: true
    receive-from-discord: true
    format-to-discord: "{player}: {message}"
    format-from-discord: "<blue>[Discord]</blue> <white>{username}</white>: <gray>{message}</gray>"
```

Replace the placeholders with your own values. The generated file has `enabled: false`; this example enables it. `global` must be a real LPC channel. After reloading, check `/lpc status` and test each intended direction.

## DiscordSRV

DiscordSRV is needed for receiving Discord chat; webhooks alone only send Minecraft messages out.

In `auto` mode with a webhook, set `use-discordsrv: true` and the numeric `discord-channel-id` for receiving. The webhook handles sending in this setup.

To use the `auto` send fallback, leave `webhook-url: ""`, keep `use-discordsrv: true` and set `discord-channel-id` to your actual numeric Discord channel ID. LPC looks it up through DiscordSRV's numeric channel API, so the same ID can be used for inbound matching. The destination must exist and be available to the bot; an unknown ID is not redirected to another channel.

Existing nonnumeric DiscordSRV **game-channel names** remain supported for outbound fallback. They do not replace the numeric ID needed to match an incoming Discord channel. If an older provider lacks the numeric lookup API, numeric AUTO sending is unavailable; compatible legacy game-channel and native relay paths remain separate options. A valid webhook still takes priority in AUTO, and `webhook` mode never switches to DiscordSRV fallback.

With `relay-mode: "discordsrv"`, match LPC channel names to DiscordSRV game-channel names (`global` is the usual starting point). DiscordSRV owns its delivery pipeline, including inbound messages; LPC does not add a second copy. The LPC webhook URL is ignored in this mode. You do not need to change DiscordSRV's `RespectChatPlugins` to use this path.

Reloading or disabling the integration retires pending LPC receive callbacks from the previous configuration. Switching to native `discordsrv` mode leaves inbound delivery with DiscordSRV, including when an old LPC callback arrives late.

## Configuration Reference

| Setting | Default | Description |
|---|---|---|
| `enabled` | `false` | Enable this integration |
| `use-discordsrv` | `true` | Allow the DiscordSRV integration |
| `relay-mode` | `auto` | Select sending behavior |
| `bot-name` | `LPC Pro` | Webhook display name |
| `avatar-url` | empty | Webhook avatar URL |
| `send-to-discord` | `true` | Forward this mapped channel outward |
| `receive-from-discord` | `true` | Allow this mapped channel's inbound path |

**To Discord:** `{player}`, `{message}`. **From Discord:** `{username}`, `{message}`.

Add another entry under `channels` for each additional mapping. A private staff destination still needs the appropriate channel permissions; an unknown LPC channel is not accepted as a destination.

## Delivery Limits

Webhook posts use a bounded queue of 500 pending messages, with up to five retries for rate limits, server errors, and connection failures. Retry headers are honored. Overflow and final failures appear in logs/status.

Pending webhook posts are discarded with a warning on reload/shutdown; the queue is not durable. A failed connection after Discord accepted a post can produce a duplicate on retry. Content is truncated to Discord's 2,000-character limit, and webhook notification mentions are disabled. Provider availability and production DiscordSRV behavior should be checked with your actual versions.
