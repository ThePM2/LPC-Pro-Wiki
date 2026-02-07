# ItemsAdder

LPC Pro integrates with [ItemsAdder](https://www.spigotmc.org/resources/itemsadder.73355/) to allow players to use custom emojis in chat messages.

## What It Enables

- **Custom Emojis** — Players can type `:emoji_name:` in chat and it renders as a custom emoji/font image defined in ItemsAdder

## Setup

1. Install ItemsAdder on your server
2. Ensure `items-adder: true` is set in `config.yml` under `hooks:`
3. Define your emojis in ItemsAdder's font_images configuration

## Usage

Players type emoji shortcodes in their messages:

```
Hello everyone :smile: How's it going? :thumbsup:
```

LPC Pro automatically replaces the `:emoji:` syntax with the corresponding ItemsAdder font image or custom stack.

## Emoji Command

| Command | Description | Permission |
|---|---|---|
| `/emoji` | View available emojis | `lpcpro.emoji` |

{% hint style="warning" %}
If both ItemsAdder and Oraxen are installed, both will process `:emoji:` syntax. It's recommended to only enable one of these integrations to avoid conflicts.
{% endhint %}
