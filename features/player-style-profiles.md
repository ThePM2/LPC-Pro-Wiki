# 👤 Player Style Profiles

Players can save several personal chat styles, preview them privately and switch between them. A profile stores **chat color, name color and the selected tag**, including supported color decorations. It does not store a rank, nickname, permissions or shop ownership.

## Commands

| Command | Description |
|---|---|
| `/chatprofile` | Open saved profiles |
| `/chatprofile save <name>` | Capture the current personal colors and selected tag |
| `/chatprofile preview <name>` | Preview a saved profile privately |
| `/chatprofile apply <name>` | Apply a saved profile |
| `/chatprofile delete <name>` | Open a deletion confirmation |
| `/chatprofile list` | List saved profiles and the current limit |
| `/chatprofile help` | Show help |

Aliases are `/chatprofiles` and `/profiles`. The command requires `lpcpro.chatprofile`, allowed by default, and is used in game.

Profile names use 1–24 letters, numbers, underscores or hyphens. Names are stored in lowercase, so `Survival` and `survival` refer to the same profile.

## Saving Your First Profile

Choose cosmetics you already have access to, then save them:

```text
/color chat green
/color name gold
/chatprofile save survival
/chatprofile preview survival
```

The example colors require the corresponding color permissions or available access through the configured cosmetic system. A selected `/tags` tag is captured too. If no manual tag is selected, the profile stores the default choice and the current automatic tag policy still applies.

Saving captures the selection at that moment. It does not change the active style. Reusing an existing name opens a replacement confirmation; later cosmetic changes do not alter the captured replacement while that confirmation is open.

## Previewing & Switching

In the menu, **left-click** a profile to preview it and **right-click** to apply it. A private preview uses the current rank and the effective channel format, with the saved personal cosmetics overlaid. The active style stays unchanged and no public message is sent.

Apply explicitly when ready:

```text
/chatprofile apply survival
```

Current permissions and shop access are checked again for saving, previewing and applying. A profile does not unlock a paid color or a revoked rank cosmetic. If any saved field is unavailable, the whole switch is refused; LPC does not apply only part of the profile.

Profiles containing a name color cannot be applied while `enable-name-color` is false. Profiles containing a tag cannot be applied while `enable-tags` is false. The saved record is kept so it can be used again when access returns.

## Profile Limits

Players can create **three profiles** by default. Grant an explicit limit permission to change this:

| Permission | Effect |
|---|---|
| `lpcpro.chatprofile` | Use saved profiles; default `true` |
| `lpcpro.chatprofile.limit.1` through `.9` | Set a creation limit from one to nine; default `false` |

The highest explicitly granted limit wins. For example, a player with both `.3` and `.5` can create five profiles. Reducing a limit does not delete existing profiles; it prevents new ones beyond the limit.

## Storage & Deletion

Profiles are saved per player in the configured database and survive reconnects and server restarts. Keep the database in normal backups.

Deleting a profile requires confirmation and removes only that saved entry. The active cosmetic selection is kept. A reload invalidates open menus and confirmations, so reopen `/chatprofile` if a view becomes stale.

Administrators changing the shared layout should use the [Chat Style Editor](chat-style-editor.md) instead.
