# 📄 Content Filter

The content filter applies moderation to signs, book pages/titles, and anvil item renames. Configuration is in `moderation/content-filter.yml`; the underlying local rules are in `moderation/moderation.yml`.

## Configuration

```yaml
filter-signs: true
filter-books: true
filter-anvil: true
block-on-filter: true
```

## Filter Behavior

| Content | Behavior |
|---|---|
| Signs and anvil names | Always reject a cancellation without replacement text. With `block-on-filter: true`, reject cancellation results even when a replacement is supplied; with `false`, use that replacement. A normal non-cancelled censoring/modification result is kept with either setting. |
| Book pages and signed titles | With `block-on-filter: true`, reject either a cancellation or a text change. With `false`, use replacement text, but still reject a cancellation that has no replacement. |

Setting `block-on-filter: false` allows a usable replacement; it does not allow an uncensorable cancellation through. A rejected sign edit is cancelled, and a rejected anvil rename has no result to take. The setting remains `true` by default. Test your selected actions on each content type when changing the policy.

## What Gets Filtered

Content runs through the non-spam moderation path, including enabled advertising, local swear, caps, cloud, and optional background AI analysis. It does not update normal chat anti-spam history. Local filters can cancel or modify the edit synchronously.

{% hint style="info" %}
AI remains post-hoc. It is not a guarantee that an already accepted sign, book, or item edit will be rolled back. Use local rules for immediate content restrictions.
{% endhint %}

## Bypass Permissions

| Permission | Description |
|---|---|
| `lpcpro.bypass.filter.sign` | Skip sign content checks |
| `lpcpro.bypass.filter.book` | Skip book content checks |
| `lpcpro.bypass.filter.anvil` | Skip anvil content checks |

Underlying filter permissions still apply when the content check runs. Use `/lpc reload` after editing the feature file.
