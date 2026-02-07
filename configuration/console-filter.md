# Console Filter

The console filter suppresses unwanted messages from the server console output. This is useful for reducing log spam from plugins or repetitive system messages. Configuration is in `moderation/console-filter.yml`.

## Configuration

```yaml
enabled: false

filters:
  # Exact match — message must equal this string
  exact: []

  # Contains — message must contain this substring
  contains: []

  # Starts-with — message must start with this string
  starts-with: []

  # Regex — message must match this pattern
  regex: []
```

## Filter Types

| Type | Description | Example |
|---|---|---|
| `exact` | Message must exactly match | `"Unknown command"` |
| `contains` | Message contains the substring | `"moved too quickly"` |
| `starts-with` | Message starts with the string | `"[ViaVersion]"` |
| `regex` | Message matches the regex pattern | `".*issued server command.*"` |

The `contains` and `regex` filter types are case-insensitive. The `exact` and `starts-with` filter types are case-sensitive.

## Examples

Suppress common console spam:

```yaml
filters:
  contains:
    - "moved too quickly"
    - "Ignoring packet"
  starts-with:
    - "[ViaVersion]"
  regex:
    - ".*lost connection: Disconnected.*"
```

## How It Works

The console filter integrates with Log4j to intercept and suppress matching log messages. Because it operates as a Log4j filter on the root logger, filtered messages may also be suppressed from log files.
