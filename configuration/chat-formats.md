# Chat Formats

Chat formats control how messages appear in chat. Each format is a YAML file in the `formats/` folder, composed of **parts** — individual text segments with their own hover tooltips and click actions.

## Format Files

| File | Purpose |
|---|---|
| `formats/chat.yml` | Default chat format (global fallback) |
| `formats/msg-sender.yml` | Private message format (sender side) |
| `formats/msg-receiver.yml` | Private message format (receiver side) |
| `formats/staff-chat.yml` | Staff channel format |
| `formats/groups/*.yml` | Group-specific format overrides |

## Structure

Each format file contains named **parts** separated by a configurable `part-separator`:

```yaml
part-separator: " "

player:
  text: "{prefix}{tag} {name}"
  hover:
    - "{prefix}{tag} {name}"
    - "&7Messages: &f%lpcpro_messages%"
    - ""
    - "&aClick to send a private message!"
  suggest: "/msg {name} "

divider:
  text: "&7➥"

message:
  text: "&f{message}"
  hover: "&eClick to report {name}'s message!"
  suggest: "/report {name} "
```

This produces chat like: `[Owner] Steve ➥ Hello everyone!`

## Part Properties

Each part supports the following properties:

### `text` (required)

The text displayed in chat. Supports placeholders, color codes, and MiniMessage formatting. Can be a string or a list of strings (joined with newlines).

### `hover`

Tooltip text shown when a player hovers over this part. Can be a single string or a list:

```yaml
hover:
  - "&bPlayer: {name}"
  - "&7World: {world}"
  - "&7Messages: %lpcpro_messages%"
```

### Click Actions

Only **one** click action per part (first match wins):

| Property | Action | Example |
|---|---|---|
| `suggest` | Pre-fills text in the chat box | `suggest: "/msg {name} "` |
| `run` | Executes a command immediately | `run: "/ignore {name}"` |
| `open` | Opens a URL in the browser | `open: "https://example.com"` |
| `copy` | Copies text to clipboard | `copy: "{name}"` |
| `click` | Generic format `ACTION:value` | `click: "SUGGEST_COMMAND:/msg {name} "` |

## Placeholders

### Built-in Placeholders

| Placeholder | Description |
|---|---|
| `{name}` / `{player}` | Player name (with nickname if set) |
| `{nickname}` | Nickname (or name if not set) |
| `{displayname}` | Player display name |
| `{prefix}` | Rank prefix (from Vault/LuckPerms) |
| `{suffix}` | Rank suffix |
| `{tag}` | Chat tag (includes leading space when set) |
| `{world}` | Current world name |
| `{message}` | The chat message content |

### PlaceholderAPI

Any `%placeholder%` from PlaceholderAPI is supported in `text` and `hover` fields. Common examples:

- `%player_first_join_date%`
- `%statistic_hours_played%`
- `%server_online%`
- `%vault_prefix%`
- `%luckperms_prefix%`

### LPC Pro Placeholders

See the full list on the [Placeholders](../placeholders.md) page.

## Formatting

LPC Pro supports multiple color and formatting syntaxes:

| Syntax | Example | Description |
|---|---|---|
| `&` codes | `&a`, `&l`, `&o` | Legacy color and formatting codes |
| MiniMessage | `<green>`, `<bold>`, `<rainbow>` | Adventure MiniMessage tags |
| Hex colors | `&#FF5555` or `<#FF5555>` | Full hex color support |
| Gradients | `<gradient:red:gold>text</gradient>` | Gradient text (MiniMessage) |

## Group-Specific Formats

You can create format overrides per group by placing files in `formats/groups/`. The file name must match the player's LuckPerms/Vault primary group name:

```
formats/groups/owner.yml   → Used for owner group
formats/groups/vip.yml     → Used for vip group
```

If no group-specific format exists, the default `formats/chat.yml` is used.

## Private Message Formats

Private message formats use additional placeholders:

**Sender format** (`msg-sender.yml`):

| Placeholder | Description |
|---|---|
| `{receiver_name}` | Name of the message recipient |

**Receiver format** (`msg-receiver.yml`):

| Placeholder | Description |
|---|---|
| `{sender_name}` | Name of the message sender |

Example sender format:

```yaml
msg:
  text: "<#6cc324>[&fme <#6cc324>➥ &f{receiver_name}<#6cc324>] &f{message}"
  hover:
    - "<#6cc324>Click to reply!"
  suggest: "/msg {receiver_name} "
```
