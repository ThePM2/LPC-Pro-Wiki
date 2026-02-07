# 🎨 Chat Formatting & Colors

LPC Pro provides rich text formatting support for chat messages, including legacy color codes, MiniMessage tags, hex colors, and gradients.

## Color Codes

### Legacy `&` Codes

| Code | Color | Code | Formatting |
|---|---|---|---|
| `&0` | Black | `&l` | **Bold** |
| `&1` | Dark Blue | `&m` | ~~Strikethrough~~ |
| `&2` | Dark Green | `&n` | <u>Underline</u> |
| `&3` | Dark Aqua | `&o` | *Italic* |
| `&4` | Dark Red | `&r` | Reset |
| `&5` | Dark Purple | | |
| `&6` | Gold | | |
| `&7` | Gray | | |
| `&8` | Dark Gray | | |
| `&9` | Blue | | |
| `&a` | Green | | |
| `&b` | Aqua | | |
| `&c` | Red | | |
| `&d` | Light Purple | | |
| `&e` | Yellow | | |
| `&f` | White | | |

### Hex Colors

Two formats are supported:

- `&#FF5555` — Ampersand hex format
- `<#FF5555>` — Angle-bracket hex format

Example: `&#FF5555Hello` produces red-colored "Hello".

### MiniMessage Format

LPC Pro supports the full [MiniMessage](https://docs.advntr.dev/minimessage/format.html) syntax:

| Tag | Example | Result |
|---|---|---|
| `<red>` | `<red>text</red>` | Red text |
| `<bold>` | `<bold>text</bold>` | Bold text |
| `<italic>` | `<italic>text</italic>` | Italic text |
| `<gradient>` | `<gradient:red:gold>text</gradient>` | Red-to-gold gradient |
| `<rainbow>` | `<rainbow>text</rainbow>` | Rainbow text |
| `<hover>` | `<hover:show_text:'tooltip'>text</hover>` | Hover tooltip |
| `<click>` | `<click:suggest_command:'/msg '>text</click>` | Click action |

## Player Permissions

Player access to formatting in chat messages is controlled by group settings and permissions:

### Group-Based (advanced/groups.yml)

| Setting | What It Controls |
|---|---|
| `can-use-colors` | Legacy `&` color codes (e.g., `&a`, `&b`) |
| `can-use-formatting` | Bold, italic, underline, strikethrough (`&l`, `&o`, `&n`, `&m`) |
| `can-use-gradients` | Gradient and rainbow formatting |

### Permission-Based

| Permission | Description |
|---|---|
| `lpcpro.message.formatting` | Bypass all individual format permissions |
| `lpcpro.message.*` | Access to all MiniMessage tags |
| `lpcpro.color.<color>` | Use a specific color (e.g., `lpcpro.color.red`) |
| `lpcpro.color.*` | Access to all colors |
| `lpcpro.color.hex` | Use hex colors |

### Available Color Permissions

Each named color has its own permission node:

`lpcpro.color.black`, `lpcpro.color.dark_blue`, `lpcpro.color.dark_green`, `lpcpro.color.dark_aqua`, `lpcpro.color.dark_red`, `lpcpro.color.dark_purple`, `lpcpro.color.gold`, `lpcpro.color.gray`, `lpcpro.color.dark_gray`, `lpcpro.color.blue`, `lpcpro.color.green`, `lpcpro.color.aqua`, `lpcpro.color.red`, `lpcpro.color.light_purple`, `lpcpro.color.yellow`, `lpcpro.color.white`

## Chat Color GUI

Players can select their preferred chat color through the GUI:

```
/color
```

This opens an inventory GUI where players can click to select their default message color. Only colors they have permission for are available.

**Permission:** `lpcpro.color`
