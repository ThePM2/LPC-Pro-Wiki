# 🌐 Chat Translation

LPC Pro translates text you submit with `/translate` using a LibreTranslate-compatible HTTP endpoint. The result is shown privately to the requesting player. Configuration is in `translation.yml`.

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/translate <text>` | `/tr`, `/trans` | Translate to your default language | `lpcpro.translate` |
| `/translate <lang> <text>` | — | Translate to a specific language | `lpcpro.translate` |
| `/translate setlang <code>` | — | Save your default target language | `lpcpro.translate` |
| `/translate languages` | — | List language codes known to LPC Pro | `lpcpro.translate` |
| `/translate reload` | — | Reload translation settings | `lpcpro.translate` + `lpcpro.translate.admin` |

## Configuration

`enable-translation` in `config.yml` is `true` by default, but `translation.yml` starts with `enabled: false`. Both switches must be enabled. A change to the main feature switch requires a restart.

The following keys are read by the current implementation:

```yaml
enabled: false

api:
  url: "https://libretranslate.com/translate"
  key: ""

translation:
  default-language: "en"

rate-limits:
  max-per-minute: 10

cache:
  max-size: 1000
  ttl-minutes: 60
```

Set the endpoint and its key for your provider, change `enabled` to `true`, then run `/lpc reload`. The URL above is the shipped default, not a promise of free or anonymous service. The endpoint receives the submitted text and target language.

## API Providers

The current request format is LibreTranslate-compatible: a JSON POST with `q`, `source`, `target`, `format` and, when configured, `api_key`. The response must contain `translatedText`; `detectedLanguage.language` is optional.

An `api.type` entry does not switch request protocols. Direct Google Translate and DeepL API support is not implemented. A self-hosted or third-party endpoint must accept the LibreTranslate request/response shape.

## Display Settings

The command shows a language header and a translation whose hover contains the original text. It does not automatically translate every incoming chat message. Entries such as `display.show-original`, `display.indicator` and `display.show-detected` in older reference files do not currently change this output.

## Rate Limiting

`rate-limits.max-per-minute` limits requests per player in a rolling one-minute window. The command accepts at most 500 characters. It does not apply a configurable `cooldown-seconds` or a `lpcpro.translate.bypass` permission.

## Caching

`cache.max-size` is clamped to 0–10,000 entries. Use `0` to stop storing new cached results. `cache.ttl-minutes` is limited to one minute–one day. `cache.enabled` is not a separate runtime switch. Reloading clears cached translations.

## Example Usage

```text
/translate languages
/translate setlang en
/translate es Hello everyone!
/translate Bonjour tout le monde!
```

The command's built-in language list includes `en`, `es`, `fr`, `de`, `it`, `pt`, `ru`, `zh`, `ja`, `ko`, `ar`, `hi`, `pl`, `nl`, `tr`, `vi`, `th`, `id`, `uk` and `sv`. Your provider must support the selected language too. `translation.available-languages` does not replace this list, and requests without an explicit source send `source: "auto"`.

## Permissions

| Permission | Description |
|---|---|
| `lpcpro.translate` | Use the translation command |
| `lpcpro.translate.admin` | Reload translation settings; also requires the base command node |

These nodes have no explicit non-operator default in the plugin descriptor. Grant access through your permission plugin. Provider reachability, language quality and paid-account access are separate from local configuration checks.
