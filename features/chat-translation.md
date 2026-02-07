# 🌐 Chat Translation

LPC Pro can translate chat messages between languages using an external translation API. Configuration is in `translation.yml`.

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/translate <text>` | `/tr`, `/trans` | Translate to your default language | `lpcpro.translate` |
| `/translate <lang> <text>` | — | Translate to a specific language | `lpcpro.translate` |
| `/translate setlang <code>` | — | Set your default target language | `lpcpro.translate` |
| `/translate languages` | — | List supported languages | `lpcpro.translate` |

## Configuration

```yaml
enabled: false

api:
  # Translation API URL
  url: "https://libretranslate.com/translate"
  # API key (if required)
  key: ""
  # API type: LIBRETRANSLATE, GOOGLE, DEEPL
  type: "LIBRETRANSLATE"

translation:
  default-language: "en"
  auto-detect: true
  available-languages:
    - "en"   # English
    - "es"   # Spanish
    - "fr"   # French
    - "de"   # German
    - "pt"   # Portuguese
    - "ru"   # Russian
    - "ja"   # Japanese
    - "ko"   # Korean
    - "zh"   # Chinese
```

## API Providers

| Provider | Config Type | Free Tier | Notes |
|---|---|---|---|
| LibreTranslate | `LIBRETRANSLATE` | Yes (self-hosted) | Open source, can self-host |
| Google Translate | `GOOGLE` | Limited | Requires API key |
| DeepL | `DEEPL` | Limited | Requires API key |

## Display Settings

```yaml
display:
  show-original: true        # Show original message on hover
  indicator: "<gray>[TR]</gray>"  # Translation indicator prefix
  show-detected: true        # Show detected source language
```

## Rate Limiting

```yaml
rate-limits:
  max-per-minute: 10         # Max translations per player per minute
  cooldown-seconds: 1        # Cooldown between translations
  bypass-permission: "lpcpro.translate.bypass"
```

## Caching

Translation results are cached to reduce API calls:

```yaml
cache:
  enabled: true
  max-size: 1000             # Maximum cached translations
  ttl-minutes: 60            # Cache expiration
```

## Permissions

| Permission | Description |
|---|---|
| `lpcpro.translate` | Use chat translation |
| `lpcpro.translate.admin` | Manage translation settings |
| `lpcpro.translate.bypass` | Bypass rate limits |
