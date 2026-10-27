# 🤖 AI Filter

The AI filter analyzes accepted chat in the background. It can alert staff without taking action, or apply post-hoc moderation after a matching result. AI is optional and disabled by default.

## Configuration

The AI filter is configured in `moderation/ai-filter.yml`:

```yaml
enabled: false
backend: "chat-completions"
mode: "enforce"
api-key: "your-api-key-here"
model: "gpt-5.6-terra"
api-endpoint: "https://api.openai.com/v1/chat/completions"
request-profile: "auto"

standard-safety:
  model: "omni-moderation-latest"
  api-endpoint: "https://api.openai.com/v1/moderations"
  categories:
    - "harassment"
    - "harassment/threatening"
    - "hate"
    - "hate/threatening"
    - "sexual/minors"

timeout-seconds: 5
toxicity-threshold: 0.7
block-toxic: false
log-analysis: false
max-requests-per-minute: 30
cache-size: 1000
cache-ttl-minutes: 30

post-hoc-moderation:
  enabled: true
  notify-staff: true
  penalty-cooldown-seconds: 30
  auto-delete-messages: true
  auto-learn-words: true
  auto-learn-threshold: 0.9
  auto-learn-min-word-length: 4
  auto-learn-min-occurrences: 3
  auto-learn-max-per-day: 10
```

## Getting Started

1. Add an API key for your chosen provider and check that the configured model is available to that account.
2. Set `enabled: true` and `mode: "observe"` for an initial trial.
3. Leave `post-hoc-moderation.enabled: true`, run `/lpc reload`, and check `/lpc status`.
4. Review the `[AI Observe]` staff alerts before choosing `mode: "enforce"`.

Provider billing, quotas, model availability, and response quality are managed by the provider. LPC Pro does not guarantee a correct verdict for every message.

## Modes

### Observe

`mode: "observe"` analyzes messages, updates usage/cache information, and can notify staff with `lpcpro.admin` or `lpcpro.mod`. It does not delete messages, add infractions, warn players, propose blocked words, or change penalty cooldowns. Your local anti-spam, swear, and other filters still apply.

### Enforce

`mode: "enforce"` can delete a tracked message after a matching result, notify staff, warn the sender, and add [infraction points](infractions.md). The default penalty cooldown is 30 seconds per player. Messages may still be deleted during that cooldown even when another infraction is not added.

{% hint style="warning" %}
AI moderation is post-hoc: players may see accepted chat before the result arrives. API errors, timeouts, quota limits, and a full request queue allow messages through. Message deletion depends on a tracked message and is unavailable on Folia. AI does not automatically send messages to the [Moderation Queue](mod-queue.md).
{% endhint %}

Setting `post-hoc-moderation.enabled: false` stops this analysis path. It does not enable a real-time blocking mode. The legacy `block-toxic` setting should not be used as a pre-send protection switch.

## Backends

| Backend | How a message matches |
|---|---|
| `chat-completions` | The model returns a toxicity decision and score, checked against `toxicity-threshold` |
| `standard-safety` | The Moderations-compatible response flags one of the selected `standard-safety.categories` |

To use the standalone Moderations protocol, set `backend: "standard-safety"`. It uses the nested model/endpoint and the same `api-key`. It does not use `toxicity-threshold`, learn words, or fall back to Chat Completions on failure. The default selected categories do not include ordinary gameplay violence or requests for help.

### Custom Providers

`request-profile: "auto"` uses the Terra request format only for the built-in Terra model at the official OpenAI Chat Completions endpoint. Other endpoints/models retain the legacy compatible request format.

Use `legacy-chat` to select the legacy request fields explicitly. `openai-terra` selects the Terra request contract for a compatible endpoint and requires `model: "gpt-5.6-terra"`. A compatible HTTP route alone does not guarantee that a provider supports the required response format.

## Word Suggestions

Despite its retained name, `auto-learn-words` only proposes candidates for staff review. It does not add words automatically. This applies to Chat Completions in Enforce mode; Observe and Standard Safety do not create suggestions.

| Command | Description |
|---|---|
| `/lpc ai suggestions` | List candidates that meet the occurrence threshold |
| `/lpc ai approve <word>` | Add a reviewed candidate to the local swear filter |
| `/lpc ai reject <word>` | Reject a candidate |

These commands require both `lpcpro.admin` and `lpcpro.ai.review`. A high sentence-level score does not establish that every word in the sentence should be blocked.

## Limits and Privacy

The default global limit is 30 requests per minute, with a separate limit of five per player and one outstanding request per player. Two calls can run while 64 wait. Responses are limited to 256 KiB, and identical results are cached for 30 minutes by default. `/lpc status` shows the active backend/mode and health counters.

`log-analysis: false` hides full message content in the AI analysis log/alert path and AI infraction reasons. AI-triggered automatic deletion follows the same captured logging choice: its log keeps the message ID, sender and a content-hidden notice, without the message body or free-form reason. With `true`, that deletion log can include the original text and reason.

This setting does not disable independent logging. Manual staff deletion logs and configured chat history have their own behavior and retention. Review [Chat History](../features/chat-history.md) when choosing what your server stores.

An enabled provider still receives the analyzed text. Keep API keys private. Players with `lpcpro.bypass.aifilter` skip this analysis path. Normal chat and enabled sign/book/anvil filtering can submit analysis; private messages use the local swear filter rather than this AI path.

## Updating an Existing Profile

Recognized retired built-in GPT-3.5 defaults at the official endpoint migrate to the Terra model when the request profile is automatic. An exact backup is saved alongside the file as `ai-filter.yml.pre-terra-<id>.bak` before an atomic replacement. Custom endpoints/models, explicit legacy profiles, API keys, enabled state, and enforcement choices are preserved. Review the startup log and `/lpc status` after updating.
