# 🤖 AI Filter

The AI filter uses OpenAI's API to analyze chat messages for toxicity. It can work as a real-time filter or in post-hoc moderation mode where flagged messages are sent to the [Moderation Queue](mod-queue.md) for staff review.

## Configuration

The AI filter is configured in `moderation/ai-filter.yml`:

```yaml
enabled: false

# OpenAI API key (required)
api-key: ""

# AI model to use
model: "gpt-3.5-turbo"

# Toxicity score threshold (0.0 - 1.0)
# Messages scoring above this are flagged
toxicity-threshold: 0.7

# API request timeout (seconds)
timeout-seconds: 5

# Translation cache settings
cache-ttl-minutes: 30

# Rate limiting
max-requests-per-minute: 30

# Post-hoc moderation mode
post-hoc-moderation:
  enabled: false
  auto-delete-messages: false
  auto-learn-words: false
```

## Modes

### Real-Time Filtering

With `post-hoc-moderation.enabled: false`, messages are analyzed before being sent to chat. Messages exceeding the toxicity threshold are blocked.

{% hint style="warning" %}
Real-time filtering adds latency to every chat message due to the API call. Consider using post-hoc mode for better player experience.
{% endhint %}

### Post-Hoc Moderation

With `post-hoc-moderation.enabled: true`, messages are sent to chat immediately and analyzed afterward. Flagged messages are sent to the [Moderation Queue](mod-queue.md) for staff review.

| Setting | Description |
|---|---|
| `auto-delete-messages` | Automatically delete messages that exceed the threshold |
| `auto-learn-words` | Add frequently flagged words to the swear filter automatically |

## Key Settings

| Setting | Default | Description |
|---|---|---|
| `toxicity-threshold` | `0.7` | Score threshold (lower = more strict) |
| `max-requests-per-minute` | `30` | API rate limit to control costs |
| `cache-ttl-minutes` | `30` | Cache identical messages to reduce API calls |
| `model` | `gpt-3.5-turbo` | OpenAI model to use |

## Requirements

- An OpenAI API key with billing enabled
- Network access from your Minecraft server to the OpenAI API
