# Swear Filter

The swear filter detects and blocks profanity in chat messages. It includes automatic evasion detection for leet speak, repeated characters, and separator characters. Configuration is in `moderation/moderation.yml`.

## Configuration

```yaml
swear-filter:
  enabled: true

  # Action: CANCEL, CENSOR, or WARN
  action: CENSOR

  # Character used for censoring
  censor-char: "*"

  # Also filter private messages
  filter-private-messages: true

  # Blocked words list
  blocked-words:
    - "word1"
    - "word2"
    # ... add your own words

  # Regex patterns for complex filtering
  blocked-patterns: []

  # Bypass permission
  bypass-permission: "lpcpro.bypass.filter"
```

## How It Works

### Word Detection

For every word in the `blocked-words` list, the filter automatically detects:

- **Exact matches** — `word`
- **Leet speak** — `w0rd`, `w@rd`, `w()rd`
- **Repeated characters** — `wooord`, `worrrd`
- **Separator characters** — `w-o-r-d`, `w.o.r.d`, `w_o_r_d`
- **Combinations** — `w0.0.r-d`

You only need to add the base word — evasion detection is automatic.

### Regex Patterns

For more complex filtering needs that can't be expressed as single words, use `blocked-patterns`:

```yaml
blocked-patterns:
  - "your.*regex.*pattern"
```

{% hint style="info" %}
The word list already handles most evasion techniques. Only use regex patterns for rules that can't be expressed as individual words.
{% endhint %}

## Actions

| Action | Description |
|---|---|
| `CANCEL` | Block the message entirely |
| `CENSOR` | Replace matched words with the censor character (default) |
| `WARN` | Allow the message but warn the player |

### Censoring Example

With `censor-char: "*"` and the word "test" blocked:

- Input: `This is a test message`
- Output: `This is a **** message`

## Private Messages

Set `filter-private-messages: true` to also filter `/msg` content through the swear filter.

## Bypass

**Permission:** `lpcpro.bypass.filter` (default: `op`)
