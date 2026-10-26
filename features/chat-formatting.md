# 🎨 Chat Formatting & Colors

LPC Pro supports legacy color codes, MiniMessage tags, hex colors and gradients. Server-owned [chat formats](../configuration/chat-formats.md) define the layout; permissions control which formatting players may type into their messages.

## Color Codes

### Legacy `&` Codes

| Code | Color | Code | Formatting |
|---|---|---|---|
| `&0` | Black | `&l` | **Bold** |
| `&1` | Dark Blue | `&m` | ~~Strikethrough~~ |
| `&2` | Dark Green | `&n` | Underline |
| `&3` | Dark Aqua | `&o` | *Italic* |
| `&4` | Dark Red | `&k` | Obfuscated |
| `&5` | Dark Purple | `&r` | Reset |
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

For example, a player with `lpcpro.message.color.green` can type `&aHello` to send green text.

### Hex Colors

Examples of supported hex notation:

- `&#FF5555Hello` — Legacy hex notation.
- `<#FF5555>Hello</#FF5555>` — MiniMessage hex notation.
- `#FF5555Hello` — Bare hex notation in supported message parsing.

Use `lpcpro.message.color.hex` for hex formatting in typed messages. The existing `lpcpro.color.hex`, `lpcpro.message.color.*` and `lpcpro.color.*` grants also allow the hex parser. Clients that cannot display RGB text may show a reduced color palette.

### MiniMessage Format

Server formats use [MiniMessage](https://docs.advntr.dev/minimessage/format.html). Typed player messages use the subset allowed by the player's permissions:

| Tag | Example | Message permission |
|---|---|---|
| Color | `<red>text</red>` | `lpcpro.message.color.red` |
| Bold | `<bold>text</bold>` | `lpcpro.message.decoration.bold` |
| Italic | `<italic>text</italic>` | `lpcpro.message.decoration.italic` |
| Gradient | `<gradient:red:gold>text</gradient>` | `lpcpro.message.gradient` |
| Rainbow | `<rainbow>text</rainbow>` | `lpcpro.message.rainbow` |
| Hover | `<hover:show_text:'More information'>text</hover>` | `lpcpro.message.hover` |
| Click | `<click:suggest_command:'/msg Steve '>text</click>` | `lpcpro.message.click` |

Grant click and hover permissions deliberately. Choosing a cosmetic in `/color` is separate from permission to add arbitrary interactive tags to a message.

## Player Permissions

### Group-Based (advanced/groups.yml)

`advanced/groups.yml` still contains the `can-use-colors`, `can-use-formatting` and `can-use-gradients` fields. These fields do not grant typed-message formatting in 2.6.0. Use the permission nodes below for that behavior.

### Permission-Based

| Permission | Description |
|---|---|
| `lpcpro.message.formatting` | Formatting override, including the standard MiniMessage tag set |
| `lpcpro.message.*` | Standard MiniMessage tag set |
| `lpcpro.message.color.<color>` | Type a named color into messages |
| `lpcpro.message.color.*` | Type any supported color into messages |
| `lpcpro.message.color.hex` | Type hex colors |
| `lpcpro.message.decoration.*` | All text decorations |
| `lpcpro.message.decoration.bold` | Bold |
| `lpcpro.message.decoration.italic` | Italic |
| `lpcpro.message.decoration.underlined` | Underline |
| `lpcpro.message.decoration.strikethrough` | Strikethrough |
| `lpcpro.message.decoration.obfuscated` | Obfuscated text |
| `lpcpro.message.reset` | Reset formatting |
| `lpcpro.message.gradient` | Gradients |
| `lpcpro.message.rainbow` | Rainbows |

In `config.yml`, `strip-unauthorized-color-codes: true` removes unauthorized legacy codes. Setting it to `false` preserves simple unauthorized `&` codes as literal text. MiniMessage tags remain permission controlled.

### Available Color Permissions

The standard named colors are `black`, `dark_blue`, `dark_green`, `dark_aqua`, `dark_red`, `dark_purple`, `gold`, `gray`, `dark_gray`, `blue`, `green`, `aqua`, `red`, `light_purple`, `yellow` and `white`.

For typed messages use `lpcpro.message.color.<name>`. For the default personal palette use `lpcpro.color.<name>`, for example `lpcpro.color.red`. Custom entries in `chat/colors.yml` can define their own `permission`.

## Chat Color GUI

Players can select a persistent personal color through:

```text
/color
```

The menu has normal, gradient and hex pages where configured. Decoration buttons combine with the selected color: changing a color keeps enabled modifiers, and toggling a modifier keeps the color. Locked entries remain unavailable, or can be hidden by their configuration.

| Command | Description |
|---|---|
| `/color` | Open the color menu |
| `/color chat red` | Set a permitted named chat color |
| `/color name gold` | Set a permitted name color |
| `/color chat #55ccff` | Set a hex color with hex access |
| `/color list` | List standard color names |
| `/color status` | Show the current selection |
| `/color reset` | Reset both chat and name colors |

Aliases are `/chatcolor`, `/namecolor` and `/colors`; they use the same subcommands. The base command requires `lpcpro.color`. Named selections require `lpcpro.color.<name>` or `lpcpro.color.*`; custom hex selections require `lpcpro.color.hex` or `lpcpro.color.*`.

`enable-name-color: false` in `config.yml` hides new name-color choices and blocks `/color name`. Existing applied name colors remain stored and displayed. A [saved player profile](player-style-profiles.md) containing a name color cannot be applied while that feature is disabled.

To offer a choice without broad formatting access, configure a permitted palette entry or an item in the [Chat Shop](chat-shop.md). Use [player style profiles](player-style-profiles.md) to save several personal selections. Administrators can change the shared layout through the [style editor and gallery](chat-style-editor.md).
