# ⚙️ Personal Chat Settings

Players can choose which ordinary public chat and chat-game messages they receive, alongside existing private-message and notification preferences. Choices are saved per player in the configured database.

## Commands

| Command | Description |
|---|---|
| `/toggle` | Show current settings and menu hints |
| `/toggle menu` | Open personal chat settings |
| `/toggle public-chat` | Toggle eligible ordinary public chat |
| `/toggle games` | Toggle public chat-game prompts and results |
| `/toggle pm` | Toggle incoming private messages |
| `/toggle mentions` | Toggle mention notifications |
| `/toggle sounds` | Toggle ordinary chat and PM sound notifications |
| `/toggle join` | Toggle join messages |
| `/toggle quit` | Toggle quit messages |
| `/toggle death` | Toggle death messages |
| `/toggle list` | List available settings |
| `/toggle gui` | Open the separate mention-sound inventory menu |

Aliases for `/toggle` are `/settings` and `/chatsettings`. The command requires `lpcpro.toggle`, allowed by default. Public-chat aliases are `public` and `chat`; the game setting also accepts `game`.

The settings menu shows controls that are available on the current server. It also offers DND when private messaging and the player's `/dnd` command access are available. Use the menu or `/dnd` for that setting; `/toggle dnd` is not a supported text subcommand.

## Public Chat

In `plugins/LPC-Pro/chat/settings.yml`:

```yaml
enabled: true
public-chat-channels:
  - global
```

The public-chat toggle applies only to listed channel IDs that have unlimited range, no permission requirement and no same-world restriction. The shipped `global` channel qualifies. Listing a protected staff or team channel does not make its messages optional public chat.

This is a receiving preference, not a mute or a command to leave channels. Private messages, staff messages, local conversations and other independent output retain their own controls. Incoming proxy channel messages also respect the preference when their local channel meets these rules.

New players receive public chat by default. Existing saved choices persist through reconnects, restarts and reloads. Setting the feature's `enabled` to `false` suspends these receiving filters while retaining stored choices for later.

## Chat Games

New players receive chat-game prompts and results by default. `/toggle games` hides the public game output produced by LPC's game broadcaster. It does not mute administrative commands or act as an opt-out from every unrelated plugin message.

The game control appears only when chat games and personal receiving controls are enabled. It is independent of `/toggle public-chat`.

## Menus & Saving

On Java, `/toggle menu` opens a private inventory menu. With a genuine current Geyser or Floodgate forms connection, the same route opens a native Bedrock form. See [Bedrock Support](../integrations/geyser.md).

Public-chat and game changes show a saving response, then confirmation after storage succeeds. If settings are still loading or storage is unavailable, wait and retry; an unavailable profile is not treated as a new player with invented choices.

For a separate mention tone, choose [Mention Sounds](mention-sounds.md). `/toggle sounds` controls chat and PM notifications and does not replace the mention tone preference. `/toggle mentions` controls eligible mention effects, including their titles.

## Placeholders

These values are available in LPC formats and through its PlaceholderAPI expansion:

| Placeholder | Result |
|---|---|
| `%lpcpro_settings_ready%` | `true` when the player's settings are loaded |
| `%lpcpro_settings_controls_available%` | `true` when the server's receiving controls are enabled and ready |
| `%lpcpro_settings_public_chat%` | Saved public-chat choice |
| `%lpcpro_settings_games%` | Saved game-output choice |
| `%lpcpro_settings_pm%` | Saved PM choice |
| `%lpcpro_settings_dnd%` | Saved DND choice |
| `%lpcpro_settings_mentions%` | Saved mentions choice |
| `%lpcpro_settings_sounds%` | Saved chat/PM sounds choice |
| `%lpcpro_settings_join%` | Saved join-message choice |
| `%lpcpro_settings_quit%` | Saved quit-message choice |
| `%lpcpro_settings_death%` | Saved death-message choice |

Preference placeholders return `true` or `false`, or `unavailable` when the player profile is not loaded. They describe saved choices; a saved `true` does not override a disabled server feature or channel access rule.
