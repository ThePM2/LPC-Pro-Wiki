# Polls

LPC Pro includes an in-chat polling system. Staff can create polls with multiple options, and players vote by clicking in chat. Configuration is in `features/polls.yml`.

## Commands

| Command | Description | Permission |
|---|---|---|
| `/poll create [duration] <question> \| <option1> \| <option2> ...` | Create a new poll | `lpcpro.poll.create` |
| `/poll vote <number>` | Vote for an option | `lpcpro.poll.vote` |
| `/poll close` | Close the active poll and show results | `lpcpro.poll.close` |
| `/poll status` | View the current poll | `lpcpro.poll` |

## Configuration

```yaml
enabled: true

max-options: 10          # Maximum choices per poll
min-options: 2           # Minimum choices per poll
default-duration: "5m"   # Default poll duration
max-duration: "7d"       # Maximum poll duration

display:
  announce-creation: true   # Announce when a poll starts
  announce-results: true    # Announce results when closed

limits:
  max-question-length: 200  # Max question characters
  max-option-length: 50     # Max option characters
```

## Creating a Poll

Use the pipe character (`|`) to separate the question from the options:

```
/poll create What gamemode should we play next? | Survival | Creative | Skyblock
```

You can specify a duration by placing it before the question:

```
/poll create 10m Best color? | Red | Blue | Green
```

## Duration Format

| Suffix | Unit |
|---|---|
| `s` | Seconds |
| `m` | Minutes |
| `h` | Hours |
| `d` | Days |

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.poll` | `true` | Base poll permission |
| `lpcpro.poll.create` | `op` | Create polls |
| `lpcpro.poll.vote` | `true` | Vote in polls |
| `lpcpro.poll.close` | `op` | Close any active poll |

## Achievements

Voting in polls contributes to poll-related achievements:

- **Voter** — Vote in 5 polls
- **Democratic** — Vote in 25 polls
