# 🔧 Initial Setup

After [installing](installation.md), start with a working layout and your existing ranks. You can add channels and moderation rules afterward.

## 1. Check Your Current Format

Run `/lpc diagnose` as a player with `lpcpro.admin`, or `/lpc diagnose Steve global` to inspect an online player's route. It explains the selected format, channel, and cosmetic precedence privately.

The selection order is an available explicit channel format, then an enabled primary-group format, then `chat`. Editing `formats/chat.yml` may have no visible effect when the player uses `formats/groups/vip.yml`.

## 2. Choose a Chat Design

```text
/lpc style gallery
```

Browse six designs. Left-click for a private preview; right-click and confirm to stage a design, then choose **Save and apply**. A preview or staged draft alone does not change public chat. Existing custom layouts require explicit adoption before replacement, and saving creates a restorable backup.

Use `/lpc style gallery vip` for a loaded format named `vip`. See [Chat Style Editor](../features/chat-style-editor.md) for editing controls and recovery.

Prefer editing YAML? This complete minimal `formats/chat.yml` needs no external placeholder expansion:

```yaml
part-separator: " "
player:
  text: "{prefix}{tag} {name}{suffix}"
  hover:
    - "<gray>World: <white>{world}"
    - "<green>Click to message"
  suggest: "/msg {name} "
divider:
  text: "<dark_gray>»"
message:
  text: "<white>{message}"
```

Run `/lpc reload` after a manual edit. To use only the generic/channel formats, set `use-group-formats: false` in `config.yml` and reload. See [Chat Formats](../configuration/chat-formats.md).

## 3. Use Your Existing Ranks

LuckPerms primary groups and prefixes can be used without recreating ranks in LPC Pro. For example:

```text
/lp group vip meta setprefix 50 "<gold>[VIP]</gold> "
```

An optional `advanced/groups.yml` `chat-prefix` overrides the provider prefix when non-empty. Its detection mode and displayed group settings are separate from format selection. Do not use its legacy color/limit fields as permission grants; see [Groups](../configuration/groups.md).

## 4. Check Channels and Player Choices

Start with the generated global channel. For a staff channel, configure an actual access permission in `chat/channels.yml`; switching to it does not grant access. The [Chat Channels](../features/chat-channels.md) guide covers complete definitions, quick prefixes, and optional automatic focus.

Players can use [style profiles](../features/player-style-profiles.md), [chat settings](../features/chat-settings.md), and [mention sounds](../features/mention-sounds.md). These are personal choices; the server format remains under administrator control.

## 5. Review Optional Features

Check the generated files before enabling external services. [AI](../moderation/ai-filter.md), [cloud downloads](../moderation/cloud-filter.md), [Discord](../integrations/discord.md), [public replies](../features/public-replies.md), and automatic announcements each have their own switches and setup. AI is disabled by default.

For a survival server, try a private style preview and a message containing `[coords]` or `[inv]`, then review the recipient and expiry rules in [Coordinates](../features/coordinates.md) and [Inventory Sharing](../features/inventory-sharing.md).

## 6. Apply and Check

Use `/lpc reload` for supported edits. Restart after changing top-level `enable...` switches or storage settings. Check `/lpc status`, try the relevant feature with an ordinary player account, and review [Commands & Permissions](../commands-and-permissions.md).
