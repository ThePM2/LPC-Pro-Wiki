# 🖼️ ItemsAdder

LPC Pro can pass chat text through ItemsAdder's font-image API so installed font images can appear in chat.

## Setup

1. Install a compatible ItemsAdder version and configure its font images/resource pack.
2. Keep `hooks.items-adder: true` in `config.yml`.
3. Check the startup log for successful hook initialization.

```yaml
hooks:
  items-adder: true
```

## Usage

Use a font-image shortcode that actually exists in your ItemsAdder configuration:

```text
Hello everyone :smile:
```

`smile` is an example name, not an image bundled with LPC Pro. Players need the provider's resource pack to see a custom image. LPC does not create the image or pack from the shortcode.

The hook prefers the player-aware API for provider permission checks. If a provider exposes only the string-only fallback, LPC logs that emoji permissions cannot be enforced by that API. Check this before using restricted images.

## Emoji Command

`/emoji` (`lpcpro.emoji`) lists LPC's configured emojis. It is not an automatic browser of every ItemsAdder font image.

When several glyph providers are enabled, give their shortcodes distinct names or enable only the one you intend to process that text. Hook availability and resource-pack rendering should be checked with your installed provider version.
