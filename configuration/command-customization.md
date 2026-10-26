# ⌨️ Command Customization

Command labels, custom actions, and command spying have separate settings. Back up the file you edit and check the startup/reload output for label conflicts.

## Rename Built-in Commands

`advanced/command-settings.yml` uses the original built-in command as its key. For example, this fragment renames the color menu:

```yaml
enabled: true
commands:
  color:
    enabled: true
    name: "chatcolor"
    aliases:
      - "ccolor"
```

Merge the entry into the existing `commands` map. `description` and `permission` can also be configured. Omitted name/alias fields retain the command's built-in values; an explicit empty alias list removes aliases. Some subcommands also check their own fixed permission, so changing the command-level permission does not grant every action.

Use `/lpc reload` and check which plugin owns the resulting label. Main `override-conflicting-commands` settings control whether LPC Pro claims contested labels; they do not rename the commands. See [Main Configuration](main-config.md) and [Commands & Permissions](../commands-and-permissions.md).

## Custom Commands

Add owner-defined commands in `features/custom-commands.yml`. This example adds a simple player-only information command:

```yaml
enabled: true
commands:
  chatguide:
    description: "Show the server's chat tips"
    player-only: true
    cooldown: 10
    aliases:
      - "chattips"
    actions:
      - type: "message"
        text: "<gold>Hello, {player}! <gray>Use /toggle menu for chat settings."
      - type: "message"
        text: "<gray>Share your location with [coords] in an ordinary channel message."
```

`cooldown` is seconds. Add `permission` and an optional `permission-message` to restrict access. Message text supports the custom-command placeholders such as `{player}`, `{displayname}`, `{uuid}`, `{world}`, `{args}`, and zero-based `{arg:0}`. This is not the normal channel pipeline: printing `[coords]` here does not capture a location or create an inventory share.

Available action types include `message`, `broadcast`, `broadcast-permission`, `console-command`, `player-command`, `sound`, `title`, `actionbar`, `teleport`, and `delay`. Text actions use `text`; command actions use `command` without a leading slash; delays use `ticks`. Console actions run with server authority. Configure only trusted commands and remember the [Folia restrictions](../getting-started/requirements.md#folia-limits).

## Command Spy

`/commandspy` is a staff tool, separate from private-message spy and persistent logging. Its `advanced/command-spy.yml` `hidden-commands` list excludes command roots such as authentication commands. The plugin also excludes its configured PM labels to keep PM text within the separate PM-spy controls.

Keep password, registration, token, and other sensitive command roots excluded, including any aliases owned by other plugins. The filter does not know every third-party command or alias automatically. See [Private Messages](../features/private-messages.md) and [Chat History & Search](../features/chat-history.md).
