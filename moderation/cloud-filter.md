# Cloud Filter

The cloud filter fetches word lists from remote sources and uses them to filter chat messages. This allows you to use community-maintained or centralized word lists that update automatically. Configuration is in `moderation/cloud-filter.yml`.

## Configuration

```yaml
enabled: false

# Automatically update word lists
auto-update: true

# Update frequency (hours)
update-interval-hours: 24

# Cache word lists locally
use-local-cache: true

# Case-sensitive matching
case-sensitive: false

# Remote word list URLs
wordlist-urls: []

# Custom regex patterns
custom-patterns: []

# Additional words to add locally
additional-words: []
```

## How It Works

1. On startup (and at each update interval), LPC Pro fetches word lists from the configured URLs
2. Downloaded lists are cached locally for reliability
3. All words from remote lists, custom patterns, and additional words are combined
4. Chat messages are checked against the combined filter

## Key Settings

| Setting | Default | Description |
|---|---|---|
| `auto-update` | `true` | Fetch updated lists periodically |
| `update-interval-hours` | `24` | How often to refresh lists |
| `use-local-cache` | `true` | Keep a local copy in case remote sources are down |
| `case-sensitive` | `false` | Whether matching is case-sensitive |

## Adding Word Lists

Add URLs to `wordlist-urls` to fetch external lists:

```yaml
wordlist-urls:
  - "https://example.com/badwords-en.txt"
  - "https://example.com/badwords-es.txt"
```

Each URL should return a plain text file with one word per line.

## Custom Patterns

Add regex patterns for advanced matching:

```yaml
custom-patterns:
  - "b[o0][t|+]"
  - "sc[a@]m"
```

## Local Additions

Add words directly without a remote source:

```yaml
additional-words:
  - "badword1"
  - "badword2"
```
