# ⛏️ Oraxen

LPC Pro integrates with [Oraxen](https://www.spigotmc.org/resources/oraxen.72448/) to allow players to use custom glyphs in chat messages.

## What It Enables

- **Custom Glyphs** — Players can type `:glyph_name:` in chat and it renders as a custom glyph defined in Oraxen

## Setup

1. Install Oraxen on your server
2. Ensure `oraxen: true` is set in `config.yml` under `hooks:`
3. Define your glyphs in Oraxen's configuration

## Usage

Players type glyph shortcodes in their messages:

```
Check this out :star: Pretty cool :heart:
```

LPC Pro automatically replaces the `:glyph:` syntax with the corresponding Oraxen glyph.

{% hint style="warning" %}
If both Oraxen and ItemsAdder are installed, both will process `:emoji:` syntax. It's recommended to only enable one of these integrations to avoid conflicts.
{% endhint %}
