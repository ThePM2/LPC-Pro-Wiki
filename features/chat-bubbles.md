# 💭 Chat Bubbles

Chat bubbles display player messages as floating text above their heads using TextDisplay entities. They need a server with TextDisplay support (Minecraft 1.19.4+) and are disabled on Folia.

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/chatbubble` | `/bubble`, `/bubbles` | Toggle your bubbles | `lpcpro.bubble` |
| `/chatbubble on` / `/chatbubble off` | — | Set your preference | `lpcpro.bubble` |
| `/chatbubble status` | — | View your preference | `lpcpro.bubble` |
| `/chatbubble enable <player>` / `/chatbubble disable <player>` | — | Set an online player's preference | `lpcpro.bubble` + `lpcpro.bubble.admin` |
| `/chatbubble reload` | — | Reload bubble settings | `lpcpro.bubble` + `lpcpro.bubble.admin` |

## How It Works

When a player sends a chat message, a TextDisplay entity appears above their head showing the message text. The bubble is removed after a configurable duration. Bubbles use smooth client-side interpolation for natural appearance.

## Features

- Per-rank/permission bubble styles
- Customizable height offset, duration, and colors
- Background colors with ARGB support
- Text shadow options
- Smooth client-side interpolation
- Automatically cleaned up on disconnect

## Permissions

| Permission | Description |
|---|---|
| `lpcpro.bubble` | Toggle chat bubbles on/off |
| `lpcpro.bubble.admin` | Manage chat bubble settings |

{% hint style="info" %}
The server must provide the TextDisplay API; older versions cannot display bubbles. Folia skips this manager and its command. The version requirement is an API requirement, not a claim that every server build or client has been visually tested.
{% endhint %}


## Configuration

Enable `enable-chat-bubbles` in `config.yml` and edit `chat/bubbles.yml`. Changing the main switch requires a restart; bubble style edits can use `/lpc reload`.

```yaml
enabled: true
require-permission: false

default:
  height-offset: 2.5
  display-duration-ticks: 100
  max-line-length: 30
  max-lines: 4
  follow-player: true
  bubble-format: "<white>%message%</white>"
  show-player-name: false
  text-shadow: false
  background-color: "0xC8333333"
  scale: 1.0
```

These are the generated default style values. `100` ticks is five seconds at 20 TPS. `%message%` is the bubble text token. `styles:` entries can override defaults and match either a `permission` or a LuckPerms/Vault `group`; the highest matching `priority` wins.

`require-permission: false` allows bubbles without a creation permission, but `/chatbubble` still requires `lpcpro.bubble`. Player bubble preferences are held in memory and reset after a server restart; use [Chat Settings](chat-settings.md) for the separately saved chat receiving preferences.
