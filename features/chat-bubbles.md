# Chat Bubbles

Chat bubbles display player messages as floating text above their heads using TextDisplay entities. Requires Paper 1.19.4+.

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/chatbubble` | `/bubble`, `/bubbles` | Toggle chat bubbles | `lpcpro.bubble` |

## How It Works

When a player sends a chat message, a TextDisplay entity appears above their head showing the message text. The bubble fades after a configurable duration. Bubbles use smooth client-side interpolation for natural appearance.

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
Chat bubbles require **Paper 1.19.4+** for TextDisplay entity support. They will not work on Spigot or older Paper versions.
{% endhint %}
