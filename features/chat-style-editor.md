# 🖌️ Chat Style Editor & Gallery

The in-game style editor lets administrators compare ready-made chat designs, preview changes privately, and save or restore a selected format. Use `/lpc style` with `lpcpro.admin`.

## Getting Started

```text
/lpc style open chat
/lpc style gallery
```

The target is the loaded **format ID**, without a directory path. `chat` selects `formats/chat.yml`. The editor changes that file only; it does not change channel mappings, group priorities or permissions.

If a player's group or channel uses a different format, editing `chat` may not change that player's normal chat. Use `/lpc diagnose <player> <channel>` to find the effective format, then open its loaded ID.

## Design Gallery

The gallery contains six designs:

| Design | Appearance |
|---|---|
| Clean SMP | Simple name and message with a `›` separator |
| Cozy Survival | World label, green separator and soft message color |
| Vanilla Plus | A familiar `<name>` layout with a colon |
| Fantasy | Decorative brackets, gold separator and a soft purple message |
| Modern | A two-line layout with an aqua divider |
| Compact | Short spacing, name first and a colon |

Left-click a design for a **private preview**. This does not replace the current draft. Right-click a design to open its confirmation screen, then confirm to stage it as a draft. **Save and apply** is still required before the selected file changes.

Designs keep rank prefixes, selected tags, nicknames and personal colors in the normal rendering flow. A personal color can override the design's message color.

## Editing a Draft

Use the menu buttons or commands:

| Command | Description |
|---|---|
| `/lpc style` | Open the current draft, or start with `chat` |
| `/lpc style open <format>` | Open a fresh draft of a loaded format |
| `/lpc style gallery [format]` | Compare the six designs |
| `/lpc style set separator <text>` | Choose `›`, `»`, `|`, `•`, `:` or `-` |
| `/lpc style set separator-color <color>` | Named MiniMessage color or `#RRGGBB` |
| `/lpc style set message-color <color>` | Named MiniMessage color or `#RRGGBB` |
| `/lpc style set hover <text>` | Set one plain hover line, up to 80 characters |
| `/lpc style set hover -` | Clear the additional hover line |
| `/lpc style preview` | Preview the current draft privately |
| `/lpc style save` | Save and apply the selected format |
| `/lpc style restore` | Restore the matching previous saved format |
| `/lpc style cancel` | Discard the draft |

For example, after choosing an editable design:

```text
/lpc style set separator »
/lpc style set separator-color #55ccff
/lpc style set message-color white
/lpc style set hover Welcome to our survival server
/lpc style preview
/lpc style save
```

Hover text is ordinary text. Formatting codes, placeholders, MiniMessage tags and `:glyph:` tokens are rejected in this field. Use a manually maintained [chat format](../configuration/chat-formats.md) for a more complex layout.

## Custom Formats

An existing custom format is initially **read-only**. It can be previewed, but the editor does not attempt to rewrite arbitrary YAML. Choose a gallery design and confirm its adoption before saving a replacement.

The **Use Clean SMP template** button opens a separate confirmation. The command equivalent is:

```text
/lpc style template confirm
```

This stages Clean SMP; it does not save. Adoption resets unsaved separator, color and hover choices to that design's defaults. Manual edits to an editor-created file also make it read-only until a design is adopted again.

## Private Preview

Only the administrator receives the preview. It is not sent to public chat, Discord, the proxy or chat logs. Click actions are removed from the preview; hover content remains available for inspection.

A preview closes the menu and keeps the draft. Reopen `/lpc style` to continue. Drafts expire after ten minutes of inactivity. Closing the ordinary editor or gallery manually discards its draft; quitting or reloading also invalidates it.

## Saving & Restoring

Before a changed format is saved, LPC preserves its exact previous bytes under `plugins/LPC-Pro/style-editor/backups/`. Backups are outside `formats/` so they are not loaded as additional layouts.

**Restore previous saved format** restores a predecessor only when it matches the current saved version. If another administrator saves, formats reload, or the file changes externally, the old draft is refused. Open a fresh draft instead of overwriting someone else's changes.

Keep the backup directory when copying a server. The editor supports up to 512 backup files per format; archive older backups if it reports that history is full. Formats and backups must be regular files no larger than 64 KiB.

For personal choices rather than a shared server layout, use [player style profiles](player-style-profiles.md).
