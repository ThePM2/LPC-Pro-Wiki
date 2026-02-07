# 🎮 Chat Games

LPC Pro includes chat games that challenge players with various game types. Games can run automatically on a schedule or be started manually by staff. Configuration is in `features/games.yml`.

## Game Types

| Type | Description |
|---|---|
| `UNSCRAMBLE` | Unscramble a jumbled word |
| `MATH` | Solve a math problem |
| `TRIVIA` | Answer a trivia question |
| `REVERSE` | Type the reversed word |
| `TYPE_RACE` | Type the given phrase fastest |
| `EMOJI_GUESS` | Guess the word from emojis |

## Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/chatgame start [type]` | `/cgame`, `/game` | Start a chat game (optionally specify type) | `lpcpro.game.start` |
| `/chatgame stop` | — | Stop the current game | `lpcpro.game.start` |
| `/chatgame random` | — | Start a random game | `lpcpro.game.start` |
| `/chatgame stats` | — | View your game statistics | `lpcpro.game.play` |
| `/chatgame top` | — | View the leaderboard | `lpcpro.game.play` |

## Configuration

```yaml
enabled: true

# Auto-start a random game every X minutes (0 = disabled)
auto-game-interval-minutes: 30

# Time limit for answering (seconds)
game-duration-seconds: 60
```

## Word List

Customize the words used in the unscramble game:

```yaml
word-list:
  - "minecraft"
  - "diamond"
  - "creeper"
  - "enderman"
  - "redstone"
  - "emerald"
  - "obsidian"
  - "skeleton"
  - "adventure"
  - "survival"
  - "enchantment"
  - "potion"
  - "villager"
  - "nether"
  - "beacon"
  - "fortress"
```

Add your own words — longer words are more challenging.

## Rewards

Configure commands that run when a player wins:

```yaml
reward-commands:
  - "give {player} diamond 1"
```

Use `{player}` as a placeholder for the winner's name.

## Messages

Customize game messages with MiniMessage formatting:

```yaml
messages:
  game-start: "<gold><bold>Chat Game!</bold></gold> <yellow>Unscramble this word: <white>{word}</white></yellow>"
  game-win: "<green>{player}</green> <yellow>won the chat game! The answer was:</yellow> <white>{answer}</white>"
  game-timeout: "<red>Time's up!</red> <yellow>The answer was:</yellow> <white>{answer}</white>"
  already-running: "<red>A game is already in progress!</red>"
```

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.game.play` | `true` | Participate in games and view stats |
| `lpcpro.game.start` | `op` | Start and stop games manually |
