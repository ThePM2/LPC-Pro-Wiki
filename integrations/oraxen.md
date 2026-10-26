# ⛏️ Oraxen

LPC Pro has an optional Oraxen glyph hook. It looks for the provider's `GlyphHandler.parse(String)` API and passes text through it when available.

## Setup

1. Install Oraxen and configure its glyphs/resource pack.
2. Keep the following in `config.yml`:

```yaml
hooks:
  oraxen: true
```

3. Check the log for successful initialization. If the installed provider no longer exposes the expected API, the hook stays unavailable rather than creating replacement glyphs.

## Usage

Use syntax and glyph names supported by your installed Oraxen version. For a provider configuration accepting a `:star:` shortcode, for example:

```text
Check this out :star:
```

The glyph and resource pack come from Oraxen, not LPC Pro. The current string-only hook does not add a separate player-aware permission check. Verify restricted glyph behavior in your provider before relying on it.

Avoid overlapping shortcodes when ItemsAdder, Oraxen, or another glyph provider processes the same text. Nexo has its own [dedicated integration](nexo.md).
