# 🏆 Achievements

The achievement system rewards players for chat milestones like message counts, mentions, replies, reputation, and poll participation. Configuration is in `features/achievements.yml`.

## Commands

| Command | Description | Permission |
|---|---|---|
| `/achievements` | Open the achievements GUI (aliases: `/achieve`, `/ach`) | `lpcpro.achievements` |

## Configuration

```yaml
enabled: true
announce-to-server: false
show-title: true

unlock-sound: "UI_TOAST_CHALLENGE_COMPLETE"
unlock-sound-volume: 1.0
unlock-sound-pitch: 1.0
```

| Setting | Type | Default | Description |
|---|---|---|---|
| `announce-to-server` | boolean | `false` | Broadcast achievement unlocks to all players |
| `show-title` | boolean | `true` | Show a title screen on unlock |
| `unlock-sound` | string | `UI_TOAST_CHALLENGE_COMPLETE` | Sound played on unlock |

## Achievement Types

| Type | Tracks | Example |
|---|---|---|
| `MESSAGE_COUNT` | Total messages sent | "Send 100 messages" |
| `UNIQUE_MENTIONS` | Different players mentioned | "Mention 10 different players" |
| `REPLIES_SENT` | Reply messages sent | "Reply to 25 messages" |
| `REPUTATION` | Reputation score | "Reach 10 reputation" |
| `POLLS_VOTED` | Polls voted in | "Vote in 5 polls" |

## Default Achievements

### Message Milestones

| Achievement | Threshold | Reward Tag |
|---|---|---|
| First Words | 1 message | `[Newbie]` |
| Chatterbox | 100 messages | `[Chatterbox]` |
| Social Butterfly | 500 messages | `[Social]` |
| Chat Veteran | 1,000 messages | `[Veteran]` |
| Legendary Speaker | 5,000 messages | `[Legend]` |
| Chat God | 10,000 messages | `[God]` |

### Social Achievements

| Achievement | Type | Threshold |
|---|---|---|
| Friendly | UNIQUE_MENTIONS | 10 players |
| Networker | UNIQUE_MENTIONS | 50 players |
| Helpful | REPLIES_SENT | 25 replies |
| Supporter | REPLIES_SENT | 100 replies |

### Reputation Achievements

| Achievement | Threshold | Reward Tag |
|---|---|---|
| Respected | 10 rep | `[Respected]` |
| Beloved | 50 rep | `[Beloved]` |
| Community Idol | 100 rep | `[Idol]` |

### Poll Achievements

| Achievement | Threshold |
|---|---|
| Voter | 5 polls |
| Democratic | 25 polls |

## Creating Custom Achievements

Add entries under `achievements:` in `achievements.yml`:

```yaml
achievements:
  my_achievement:
    name: "Chat Master"
    description: "Send 2,500 messages"
    type: MESSAGE_COUNT
    threshold: 2500
    reward-tag: "<gradient:gold:yellow>[Master]</gradient>"
    reward-commands:
      - "give {player} diamond 5"
      - "eco give {player} 1000"
```

### Achievement Properties

| Property | Required | Description |
|---|---|---|
| `name` | Yes | Display name |
| `description` | Yes | Description text |
| `type` | Yes | Achievement type (see table above) |
| `threshold` | Yes | Value needed to unlock |
| `reward-tag` | No | MiniMessage-formatted tag granted on unlock |
| `reward-commands` | No | Commands to execute on unlock (`{player}` placeholder) |

## Placeholders

| Placeholder | Description |
|---|---|
| `%lpcpro_achievements%` | Progress (e.g., "5/15") |
| `%lpcpro_achievements_unlocked%` | Unlocked count |
| `%lpcpro_achievements_total%` | Total achievements |
| `%lpcpro_achievements_percent%` | Unlock percentage (e.g., "33%") |
