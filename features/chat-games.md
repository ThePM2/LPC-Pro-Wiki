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
| `/chatgame start [type]` | `/cgame`, `/game` | Start a game (defaults to `math`) | `lpcpro.game.play` + `lpcpro.game.start` |
| `/chatgame stop` | — | Stop the current game | `lpcpro.game.play` + `lpcpro.game.start` |
| `/chatgame random` | — | Start a random game | `lpcpro.game.play` + `lpcpro.game.start` |
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
  game-start:
    math: "<gold><bold>MATH</bold></gold> <yellow>Solve: <white>{problem} = ?</white></yellow>"
    unscramble: "<aqua><bold>UNSCRAMBLE</bold></aqua> <yellow>Unscramble: <white>{word}</white></yellow>"
    trivia: "<light_purple><bold>TRIVIA</bold></light_purple> <white>{question}</white>"
    reverse: "<green><bold>REVERSE</bold></green> <white>{word}</white>"
    type_race: "<yellow><bold>TYPE RACE</bold></yellow> <white>{phrase}</white>"
    emoji_guess: "<light_purple><bold>EMOJI GUESS</bold></light_purple> <white>{category}: {emoji}</white>"
  game-win: "<green>{player}</green> <yellow>won the chat game! The answer was:</yellow> <white>{answer}</white>"
  game-timeout: "<red>Time's up!</red> <yellow>The answer was:</yellow> <white>{answer}</white>"
  cancelled: "<red>Game cancelled.</red>"
  already-running: "<red>A game is already in progress!</red>"
```

## Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.game.play` | `true` | Participate in games and view stats |
| `lpcpro.game.start` | `op` | Start and stop games manually |


## Playing and Receiving Games

Both `enable-chat-games` in `config.yml` and `enabled` in `features/games.yml` must be on. The main switch requires a restart; edit the schedule, rewards or message templates and run `/lpc reload`.

For a quick manual game, use `/chatgame start math`, then type the answer in ordinary chat. The first accepted correct answer wins. Only one game runs at a time. `auto-game-interval-minutes: 0` stops automatic games while keeping manual games available.

Players can hide game broadcasts through `/toggle games` when receiving controls are enabled. This is separate from private messages and ordinary chat. Title timing can be configured with `title.enabled`, `title.fade-in`, `title.stay` and `title.fade-out`; the shipped values are `true`, `5`, `60` and `10` ticks.

The `messages.game-start` section uses one entry per game type. Keep placeholders with their matching template: math uses `{problem}`, trivia uses `{question}`, type race uses `{phrase}`, emoji guess uses `{category}` and `{emoji}`, and word games use `{word}`. The YAML above is an example design, not a replacement for the full word list or generated messages.

Reward commands run from console. On Folia they remain blocked by default through `folia.allow-unsafe-console-commands`; enable that only for commands you have checked for Folia safety. A code path accepting a game type does not certify every client animation or sound.
