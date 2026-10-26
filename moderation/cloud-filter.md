# ☁️ Cloud Filter

The cloud filter downloads word lists and combines them with your local words and patterns. It is configured separately from the local swear filter in `moderation/cloud-filter.yml`.

## Configuration

The bundled configuration enables English, Spanish, and German lists:

```yaml
enabled: true
auto-update: true
update-interval-hours: 24
use-local-cache: true
case-sensitive: false
wordlist-urls:
  - "https://raw.githubusercontent.com/LDNOOBW/List-of-Dirty-Naughty-Obscene-and-Otherwise-Bad-Words/master/en"
  - "https://raw.githubusercontent.com/LDNOOBW/List-of-Dirty-Naughty-Obscene-and-Otherwise-Bad-Words/master/es"
  - "https://raw.githubusercontent.com/LDNOOBW/List-of-Dirty-Naughty-Obscene-and-Otherwise-Bad-Words/master/de"
custom-patterns: []
additional-words: []
```

## How It Works

Enabled normal/content moderation censors matches from the combined list. Downloads do not upload player messages. `enabled: false` stops cloud filtering and refresh requests.

Each URL has its own cache. Removing a URL removes its words after reload. If a refresh fails, only that source's previous data and success time are retained. Old merged `cloud-filter-cache.txt` files are not imported; an upgrade from that format needs a successful refresh for remote words.

{% hint style="info" %}
`swear-filter.enabled` and `lpcpro.bypass.filter` control the local swear filter, not this separate cloud stage. Configure or disable the cloud filter independently. Normal private messages do not use this cloud stage.
{% endhint %}

## Adding Word Lists

Use HTTPS URLs that return plain text with one word per line. There can be at most 32 sources, with a limit of 4 MiB and 20,000 words per source. Keep the existing URLs when adding another list if you want to retain their words.

## Custom Patterns

```yaml
custom-patterns:
  - 'sc[a@]m'
```

Patterns use Java regular expressions. Up to 100 patterns are accepted, each no longer than 512 characters. Start with a small list and check for unintended matches.

## Local Additions

```yaml
additional-words:
  - "exampleblockedword"
```

Run `/lpc reload` after changes and use `/lpc status` to inspect cloud health. Remote list availability is independent of LPC Pro.
