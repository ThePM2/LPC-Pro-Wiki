# 🧩 Nexo

LPC Pro supports Nexo's available MiniMessage glyph and shift tag resolvers. The integration is separate from the Oraxen hook.

## Setup

1. Install Nexo and configure its glyphs/resource pack.
2. Keep this setting in `config.yml`:

```yaml
hooks:
  nexo: true
```

3. Restart after installing the provider and check for `Nexo hook initialized` in the log. `/lpc reload` reloads the hook setting.

## Usage

Use the glyph/shift tags exposed by your installed Nexo version in supported MiniMessage text. LPC asks Nexo for player-aware resolvers when available, then for the provider's shared resolver APIs. It does not bundle Nexo glyph definitions or a resource pack.

If your chosen Nexo placeholders use `%nexo_...%`, install/configure their PlaceholderAPI support as well. LPC's Nexo hook does not generate missing PAPI expansions.

## Troubleshooting

If tags remain unresolved, check that the provider exposes a supported resolver and that the player has its required access. If an image renders as a missing character, check the Nexo pack on the client. Enabling a hook does not translate a Java resource pack into a Bedrock pack.
