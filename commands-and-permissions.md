# ⌨️ Commands & Permissions

Complete reference of LPC Pro 2.6.0 commands and permissions.

Commands below use the built-in names and aliases. Servers can rename or disable them in `advanced/command-settings.yml`; examples assume the defaults. Feature switches and service health can also make a command unavailable. See [Main Configuration](configuration/main-config.md) for feature switches.

{% hint style="info" %}
Subcommands need their command's base permission as well as any extra permission shown below. For example, channel muting needs both `lpcpro.mute` and `lpcpro.mute.channel`; poll creation needs both `lpcpro.poll` and `lpcpro.poll.create`. All `/lpc` subcommands, including help, require `lpcpro.admin`.
{% endhint %}

## Core Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/lpcpro` | `/lpc` | Main plugin command and help | `lpcpro.admin` |
| `/lpc reload` | — | Reload supported configuration files; top-level feature switches and database changes need a restart | `lpcpro.admin` + `lpcpro.command.reload` |
| `/lpc help [page]` | — | Show help menu | `lpcpro.admin` |
| `/lpc status` | — | Service health, storage queues and chat counters | `lpcpro.admin` |
| `/lpc info` | `/lpc about` | Version, features and hooks | `lpcpro.admin` |
| `/lpc diagnose [player] [channel]` | — | Explain your setup or an exact online player's route; console must name a player | `lpcpro.admin` |
| `/lpc style` | — | Open the administrator's private format editor | `lpcpro.admin` |
| `/lpc ai suggestions` | — | List AI word suggestions for manual review | `lpcpro.admin` + `lpcpro.ai.review` |
| `/lpc ai approve <word>` | — | Approve a supported word suggestion | `lpcpro.admin` + `lpcpro.ai.review` |
| `/lpc ai reject <word>` | — | Remove a word suggestion | `lpcpro.admin` + `lpcpro.ai.review` |

## Messaging Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/msg <player> <message>` | `/m`, `/tell`, `/t`, `/whisper`, `/w` | Send a private message | `lpcpro.command.msg` |
| `/r <message>` | `/reply` | Reply to last message | `lpcpro.command.reply` |
| `/ignore <player>` | — | Ignore a player | `lpcpro.command.ignore` |
| `/unignore <player>` | — | Unignore a player | `lpcpro.command.unignore` |

## Channel Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/channel join <name>` | `/ch`, `/chat` | Join a channel | `lpcpro.channel` |
| `/channel leave <name>` | — | Leave a channel | `lpcpro.channel` |
| `/channel list` | — | List available channels | `lpcpro.channel` |
| `/channel switch <name>` | — | Switch active write channel | `lpcpro.channel` |
| `/channel <name>` | — | Quick switch to a channel (joins if needed) | `lpcpro.channel` |
| `/qch <channel> <message>` | — | Send once without changing your write channel | `lpcpro.channel.quick` |
| `/channel focus <channel>` | — | Alias of `/channel switch <channel>` | `lpcpro.channel` |
| `/channel auto` | — | Resume automatic channel focus from configured permission rules | `lpcpro.channel` |

## Moderation Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/mute <player> [duration] [reason]` | — | Mute a player | `lpcpro.mute` |
| `/mute channel <channel> [duration] [reason]` | — | Mute a channel | `lpcpro.mute.channel` |
| `/mute server [duration] [reason]` | — | Mute entire server chat | `lpcpro.mute.server` |
| `/unmute <player>` | — | Unmute a player | `lpcpro.mute` |
| `/unmute channel <channel>` | — | Unmute a channel | `lpcpro.mute.channel` |
| `/unmute server` | — | Unmute server chat | `lpcpro.mute.server` |
| `/mutes [player]` | `/mutehistory` | View mute history (own if no player) | `lpcpro.mute.view` |
| `/warn <player> [points] <reason>` | — | Issue a warning (default 1 point) | `lpcpro.warn` |
| `/warnings [player]` | `/warns` | View warnings (own if no player) | `lpcpro.warn.view` |
| `/warnings remove <player> #<n>` | — | Remove a specific warning | `lpcpro.warn.remove` |
| `/warnings clear <player>` | — | Clear all warnings for a player | `lpcpro.warn.clear` |
| `/warnings top` | — | Show most-warned players | `lpcpro.warn.view` |
| `/report <player> [reason]` | — | Report a player | `lpcpro.report` |
| `/reports` | — | View pending reports | `lpcpro.reports.view` |
| `/reports list [status]` | — | List reports by status (pending/resolved/dismissed) | `lpcpro.reports.view` |
| `/reports view <id>` | — | View report details | `lpcpro.reports.view` |
| `/reports resolve <id> [note]` | — | Resolve a report | `lpcpro.reports.manage` |
| `/reports dismiss <id> [note]` | — | Dismiss a report | `lpcpro.reports.manage` |
| `/reports player <name>` | — | View reports against a player | `lpcpro.reports.view` |
| `/clearchat [silent] [reason]` | `/cc`, `/chatclear` | Clear the chat (use `silent` to hide staff name) | `lpcpro.clearchat` |
| `/announce <message>` | `/broadcast`, `/bc` | Send a server announcement | `lpcpro.announce` |
| `/slowmode <seconds\|off\|status>` | `/slow` | Set, disable, or check slowmode | `lpcpro.slowmode` |
| `/deletemsg <messageId>` | `/delmsg`, `/removemsg` | Delete a chat message | `lpcpro.chat.delete` |
| `/modqueue` | `/mq`, `/modq` | List pending moderation queue | `lpcpro.modqueue` |
| `/modqueue view <id>` | — | View a specific queued message | `lpcpro.modqueue` |
| `/modqueue approve <id>` | — | Approve a queued message | `lpcpro.modqueue` |
| `/modqueue deny <id>` | — | Deny a queued message | `lpcpro.modqueue` |
| `/modqueue denywarn <id>` | — | Deny and warn the player | `lpcpro.modqueue` |
| `/modqueue clear` | — | Clear all pending messages | `lpcpro.modqueue` + `lpcpro.modqueue.admin` |
| `/modqueue toggle` | — | Toggle the moderation queue on/off | `lpcpro.modqueue` + `lpcpro.modqueue.admin` |
| `/infractions <player>` | — | View active infractions and points | `lpcpro.infractions` |
| `/infractions history <player>` | — | View active and expired infractions | `lpcpro.infractions` |
| `/infractions top` | — | List players by active points | `lpcpro.infractions` |
| `/infractions remove <player> #<id>` | — | Remove a stored infraction by its ID | `lpcpro.infractions` |
| `/infractions clear <player>` | — | Clear a player's infractions | `lpcpro.infractions` |
| `/raidmode [on\|off\|status]` | `/raid`, `/raidprotection` | Toggle or check raid mode | `lpcpro.raidmode` |
| `/raidmode trust <player>` | — | Add player to trusted list | `lpcpro.raidmode` |
| `/raidmode untrust <player>` | — | Remove player from trusted list | `lpcpro.raidmode` |
| `/raidmode trusted` | — | List trusted players | `lpcpro.raidmode` |
| `/newcomer status <player>` | `/newbie`, `/nc` | Check newcomer status | `lpcpro.newcomer.admin` |
| `/newcomer graduate <player>` | — | Graduate a player from newcomer | `lpcpro.newcomer.admin` |
| `/newcomer reset <player>` | — | Reset player to newcomer status | `lpcpro.newcomer.admin` |
| `/newcomer reload` | — | Reload newcomer configuration | `lpcpro.newcomer.admin` |

## Social Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/rep <player>` | `/reputation`, `/+rep` | Give configured reputation points (default +1) | `lpcpro.rep.give` |
| `/rep view [player]` | — | View reputation (own if no player) | `lpcpro.rep.view` |
| `/rep top` | — | Reputation leaderboard | `lpcpro.rep.top` |
| `/poll create [duration] <question> \| <options>` | — | Create a poll | `lpcpro.poll.create` |
| `/poll vote <number>` | — | Vote in a poll | `lpcpro.poll.vote` |
| `/poll close` | — | Close a poll | `lpcpro.poll.close` |
| `/poll status` | — | Show the active poll | `lpcpro.poll` |
| `/achievements [player]` | `/achieve`, `/ach` | Open your own or another player's achievements GUI | `lpcpro.achievements` |
| `/achievements grant <player> <id>` | — | Unlock an achievement for an online player and run its rewards | `lpcpro.achievements` + `lpcpro.achievements.admin` |
| `/achievements revoke <player> <id>` | — | Remove an unlock, including for a known offline player | `lpcpro.achievements` + `lpcpro.achievements.admin` |
| `/chatgame start [type]` | `/cgame`, `/game` | Start a chat game | `lpcpro.game.start` |
| `/chatgame stats` | — | View game stats | `lpcpro.game.play` |
| `/chatgame random` | — | Start a random game | `lpcpro.game.play` + `lpcpro.game.start` |
| `/chatgame stop` | — | Stop the active game | `lpcpro.game.play` + `lpcpro.game.start` |
| `/chatgame top` | — | Game wins leaderboard | `lpcpro.game.play` |
| `/mail [page]` | `/email` | View your inbox | `lpcpro.mail` |
| `/mail send <player> <message>` | `/email` | Send mail | `lpcpro.mail` |
| `/mail read <id>` | — | Read a specific mail | `lpcpro.mail` |
| `/mail reply <id> <message>` | — | Reply to mail | `lpcpro.mail` |
| `/mail delete <id>` | — | Delete a mail | `lpcpro.mail` |
| `/mail clear` | — | Clear your mail | `lpcpro.mail` |
| `/qr <name>` | `/quickreply`, `/quickreplies` | Send a saved quick reply | `lpcpro.quickreply` |
| `/qr add <name> <message>` | — | Save a quick reply | `lpcpro.quickreply` |
| `/qr list` | — | List your quick replies | `lpcpro.quickreply` |
| `/qr remove <name>` | — | Delete a quick reply | `lpcpro.quickreply` |

## Shop & Economy Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/chatshop` | `/cshop`, `/perkshop`, `/chatstore` | Open shop GUI | `lpcpro.shop` |
| `/chatshop balance` | — | Check currency balance | `lpcpro.shop` |
| `/chatshop colors` | — | Browse chat colors | `lpcpro.shop` |
| `/chatshop names` | — | Browse name colors | `lpcpro.shop` |
| `/chatshop tags` | — | Browse tags | `lpcpro.shop` |
| `/chatshop perks` | — | Browse perks | `lpcpro.shop` |
| `/chatshop give <player> <amount>` | — | Give currency (admin) | `lpcpro.shop.admin` |
| `/chatshop set <player> <amount>` | — | Set currency (admin) | `lpcpro.shop.admin` |
| `/chatshop take <player> <amount>` | — | Take currency (admin) | `lpcpro.shop.admin` |
| `/chatshop recover <player> <item-id> <paid\|not-paid>` | — | Resolve a pending purchase after checking the economy ledger | `lpcpro.shop` + `lpcpro.shop.admin` |

## Customization Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/color` | `/chatcolor`, `/namecolor`, `/colors` | Open color selection GUI | `lpcpro.color` |
| `/color chat <color>` | — | Set a permitted chat color | `lpcpro.color` + color access |
| `/color name <color>` | — | Set a permitted name color when enabled | `lpcpro.color` + color access |
| `/color reset` | — | Clear both selected colors | `lpcpro.color` |
| `/color list` | — | List named colors and permitted hex access | `lpcpro.color` |
| `/color status` | — | View current chat/name colors | `lpcpro.color` |
| `/nick <nickname>` | `/nickname`, `/setnick` | Set your nickname | `lpcpro.nick` |
| `/nick off` | — | Remove your nickname | `lpcpro.nick` |
| `/tags` | `/tag`, `/chattags`, `/nametag` | Open tag selection GUI | `lpcpro.tags` |
| `/emoji [list\|category\|search] [value]` | `/emojis`, `/emote`, `/emotes` | Browse emojis | `lpcpro.emoji` |
| `/toggle` | `/settings`, `/chatsettings` | List your receiving preferences | `lpcpro.toggle` |
| `/toggle <setting>` | — | Toggle one supported preference | `lpcpro.toggle` |
| `/toggle menu` | — | Open settings (native form for a connected Bedrock player) | `lpcpro.toggle` |
| `/toggle mention-sound [preview] <preset>` | — | Preview or select `default`, `chime`, `bell` or `silent` | `lpcpro.toggle` |
| `/chatprofile` | `/chatprofiles`, `/profiles` | Open your saved style profiles | `lpcpro.chatprofile` |
| `/chatprofile save <name>` | — | Save current colors/tag; replacing an existing profile opens confirmation | `lpcpro.chatprofile` |
| `/chatprofile preview <name>` | — | Preview privately | `lpcpro.chatprofile` |
| `/chatprofile apply <name>` | — | Apply currently permitted cosmetics from a saved profile | `lpcpro.chatprofile` |
| `/chatprofile delete <name>` | — | Open confirmation to delete a saved profile | `lpcpro.chatprofile` |
| `/chatprofile list` | — | List your saved profiles | `lpcpro.chatprofile` |
| `/chatmenu` | — | Open recently delivered chat actions on a connected Bedrock client | `lpcpro.chatmenu` |
| `/lpcview <token>` | — | Open a snapshot from its delivered chat action | Snapshot-type view permission |
| `/chatreply <token> <message>` | — | Reply publicly using a recent message's action | `lpcpro.chat.reply.public` |
| `/dnd [on\|off]` | `/donotdisturb` | Toggle or set Do Not Disturb | `lpcpro.dnd` |
| `/dnd message <message>` | — | Set the DND auto-reply | `lpcpro.dnd` |
| `/chatbubble` | `/bubble`, `/bubbles` | Toggle chat bubbles | `lpcpro.bubble` |
| `/chatbubble on` / `/chatbubble off` / `/chatbubble status` | — | Set or view your bubble preference | `lpcpro.bubble` |
| `/chatbubble enable <player>` / `/chatbubble disable <player>` | — | Set an online player's bubble preference | `lpcpro.bubble` + `lpcpro.bubble.admin` |
| `/chatbubble reload` | — | Reload bubble styles | `lpcpro.bubble` + `lpcpro.bubble.admin` |
| `/translate <text>` | `/tr`, `/trans` | Translate text to your language | `lpcpro.translate` |
| `/translate <lang> <text>` | — | Translate to specific language | `lpcpro.translate` |
| `/translate setlang <code>` | — | Set your default language | `lpcpro.translate` |
| `/translate languages` | — | List language codes known to the command | `lpcpro.translate` |
| `/translate reload` | — | Reload translation configuration | `lpcpro.translate` + `lpcpro.translate.admin` |
| `/macro <name>` | `/macros` | Send a saved macro message | `lpcpro.macro` |
| `/macro list` | — | List all macros | `lpcpro.macro` |
| `/macro set <name> <message>` | — | Create/update a global macro | `lpcpro.macro.admin` |
| `/macro remove <name>` | — | Remove a global macro from the running list | `lpcpro.macro.admin` |
| `/macro personal <name> <message>` | — | Create a personal macro | `lpcpro.macro` |
| `/macro personal <name> -` | — | Remove your session-only macro | `lpcpro.macro` |

## Staff Utility Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/chathistory <player> [count]` | `/chatlogs`, `/clogs` | View a player's chat history | `lpcpro.chatlog.view` |
| `/chathistory channel <id> [count]` | — | View channel history | `lpcpro.chatlog.view` |
| `/chatsearch <query>` | `/csearch`, `/searchchat`, `/findchat` | Search chat logs | `lpcpro.chatlog.search` |
| `/chatsearch player:<name> [query]` | — | Search by player | `lpcpro.chatlog.search` |
| `/chatsearch channel:<id> [query]` | — | Search by channel | `lpcpro.chatlog.search` |
| `/chatsearch time:<duration> [query]` | — | Search within time range | `lpcpro.chatlog.search` |
| `/spy` | — | Toggle private message spy | `lpcpro.spy.pm` |
| `/channelspy <channel>` | `/cspy` | Toggle spy for a channel | `lpcpro.spy.channel` |
| `/commandspy` | `/cmdspy` | Toggle command spy | `lpcpro.spy.command` |
| `/chatgroup` | `/cgroup`, `/groups` | View your group | `lpcpro.group` |
| `/chatgroup list` | — | List all groups | `lpcpro.group` |
| `/chatgroup info <group>` | — | View group details | `lpcpro.group` |
| `/chatgroup check <player>` | — | Check player's group (admin) | `lpcpro.group.admin` |
| `/chatgroup reload` | — | Reload group configuration (admin) | `lpcpro.group.admin` |
| `/note add <player> <note>` | — | Add a note to a player | `lpcpro.note.add` |
| `/note list <player>` | — | View player notes | `lpcpro.note.view` |
| `/note remove <id>` | — | Remove a note by ID | `lpcpro.note.remove` |
| `/note clear <player>` | — | Clear all notes for a player | `lpcpro.note.clear` |

---

## Console Usage

Console supports `/lpc`, `/announce`, `/clearchat`, `/mute`, `/unmute`, `/warn`, `/raidmode`, `/slowmode`, `/chatsearch` and the `grant`/`revoke` achievement actions. The other commands in this reference require an in-game player. `/lpc style` also needs a player for its private editor.

`/lpcview` and `/chatreply` tokens are created for messages actually delivered to your current session. Use the chat action or Bedrock menu; copying someone else's token does not grant access. Inventory previews, managed deletion and public replies are unavailable on Folia.

---

## All Permissions

`true` means granted by the plugin to all players; `op` means operators by default; `false` means not granted automatically. `—` means the node has no explicit default in LPC Pro's `plugin.yml`: grant it explicitly in your permission plugin. A configurable permission can differ from the node shown here.

For example, the default descriptor does **not** grant `lpcpro.tags`, `lpcpro.mail`, `lpcpro.quickreply`, `lpcpro.achievements` or `lpcpro.shop` to every non-operator. Give players the feature access you want them to have.

```text
/lp group default permission set lpcpro.tags true
/lp group default permission set lpcpro.mail true
/lp group default permission set lpcpro.chatprofile true
```

### General

| Permission | Default | Description |
|---|---|---|
| `lpcpro.command.reload` | `op` | Reload the plugin |
| `lpcpro.admin` | `op` | Access admin commands |
| `lpcpro.staff` | — | Staff permission |
| `lpcpro.staff.alert` | — | Staff alert notifications |

### Messaging

| Permission | Default | Description |
|---|---|---|
| `lpcpro.command.msg` | `true` | Send private messages |
| `lpcpro.command.reply` | `true` | Reply to messages |
| `lpcpro.command.ignore` | `true` | Ignore players |
| `lpcpro.command.ignore.bypass` | `op` | Prevent new ignores while online; does not override an already saved ignore |
| `lpcpro.command.unignore` | `true` | Unignore players |
| `lpcpro.dnd` | `true` | Toggle Do Not Disturb |
| `lpcpro.toggle` | `true` | Toggle chat settings |

### Channels

| Permission | Default | Description |
|---|---|---|
| `lpcpro.channel` | `true` | Use channel commands |
| Channel's configured `permission` | — | Access a restricted channel (read and join/send authorization) |
| `lpcpro.channel.deny.speak.<channel>` | — | Explicitly deny speaking; operators/admins bypass this denial |

### Moderation

| Permission | Default | Description |
|---|---|---|
| `lpcpro.mute` | `op` | Mute/unmute players |
| `lpcpro.mute.channel` | `op` | Mute/unmute channels |
| `lpcpro.mute.server` | `op` | Mute/unmute server |
| `lpcpro.mute.view` | `op` | View mute history |
| `lpcpro.warn` | `op` | Issue warnings |
| `lpcpro.warn.view` | `op` | View warnings |
| `lpcpro.warn.remove` | `op` | Remove warnings |
| `lpcpro.warn.clear` | `op` | Clear all warnings |
| `lpcpro.warn.bypass` | `op` | Bypass warning thresholds |
| `lpcpro.report` | `true` | Report players |
| `lpcpro.reports.view` | `op` | View reports |
| `lpcpro.reports.manage` | `op` | Manage reports |
| `lpcpro.clearchat` | `op` | Clear chat |
| `lpcpro.clearchat.bypass` | `op` | Bypass chat clear |
| `lpcpro.chat.delete` | `op` | Delete individual messages |
| `lpcpro.announce` | `op` | Send announcements |
| `lpcpro.slowmode` | `op` | Manage slowmode |
| `lpcpro.slowmode.bypass` | `op` | Bypass slowmode |

### Bypass

| Permission | Default | Description |
|---|---|---|
| `lpcpro.bypass.mute` | `op` | Bypass mute |
| `lpcpro.bypass.spam` | `op` | Bypass anti-spam |
| `lpcpro.bypass.caps` | `op` | Bypass anti-caps |
| `lpcpro.bypass.advertising` | `op` | Bypass anti-advertising |
| `lpcpro.bypass.filter` | `op` | Bypass swear filter |
| `lpcpro.bypass.grammar` | `op` | Bypass auto-grammar |

### Spy

| Permission | Default | Description |
|---|---|---|
| `lpcpro.spy.pm` | `op` | Spy on private messages |
| `lpcpro.spy.channel` | `op` | Spy on channels |
| `lpcpro.spy.bypass` | `false` | Your messages hidden from spies |
| `lpcpro.spy.silent` | `op` | See silently cancelled messages |

### Social

| Permission | Default | Description |
|---|---|---|
| `lpcpro.rep` | `true` | Base rep permission |
| `lpcpro.rep.give` | `true` | Give reputation |
| `lpcpro.rep.view` | `true` | View reputation |
| `lpcpro.rep.top` | `true` | View leaderboard |
| `lpcpro.rep.bypass.cooldown` | — | Bypass rep cooldown |
| `lpcpro.poll` | `true` | Base poll permission |
| `lpcpro.poll.create` | `op` | Create polls |
| `lpcpro.poll.vote` | `true` | Vote in polls |
| `lpcpro.poll.close` | `op` | Close polls |
| `lpcpro.mention` | `true` | Mention players |
| `lpcpro.mention.receive` | `true` | Receive mention notifications |
| `lpcpro.mention.everyone` | `op` | Use @everyone and @here |
| `lpcpro.mail` | — | Use mail commands |
| `lpcpro.quickreply` | — | Use quick reply commands |
| `lpcpro.quickreply.extra` | — | Access extra quick reply slots |
| `lpcpro.group` | — | View group information |
| `lpcpro.group.admin` | — | Manage groups (check player, reload) |

### Customization

| Permission | Default | Description |
|---|---|---|
| `lpcpro.color` | `true` | Open color GUI |
| `lpcpro.color.*` | `op` | All colors |
| `lpcpro.color.hex` | `op` | Hex colors |
| `lpcpro.nick` | `true` | Set nickname |
| `lpcpro.nick.color` | `op` | Colors in nickname |
| `lpcpro.nick.others` | `op` | Declared compatibility node; the current command only sets your own nickname |
| `lpcpro.message.*` | `op` | Access to all message formatting tags |
| `lpcpro.message.formatting` | `op` | All formatting codes |
| `lpcpro.emoji` | `true` | View emojis |
| `lpcpro.tags` | — | Open tag selection GUI |
| `lpcpro.achievements` | — | View achievements GUI |

### Staff Notes

| Permission | Default | Description |
|---|---|---|
| `lpcpro.note` | `op` | Base note permission |
| `lpcpro.note.add` | `op` | Add notes |
| `lpcpro.note.view` | `op` | View notes |
| `lpcpro.note.remove` | `op` | Remove notes |
| `lpcpro.note.clear` | `op` | Clear notes |
| `lpcpro.note.notify` | `op` | Notified when noted players join |

### Chat Logs

| Permission | Default | Description |
|---|---|---|
| `lpcpro.chatlog.view` | `op` | View chat logs |
| `lpcpro.chatlog.search` | `op` | Search chat logs |

### Tags

| Permission | Default | Description |
|---|---|---|
| `lpcpro.autotag.staff` | `false` | Auto-equip Staff tag |
| `lpcpro.autotag.helper` | `false` | Auto-equip Helper tag |
| `lpcpro.autotag.trial-mod` | `false` | Auto-equip Trial-Mod tag |
| `lpcpro.autotag.mod` | `false` | Auto-equip Mod tag |
| `lpcpro.autotag.admin` | `false` | Auto-equip Admin tag |
| `lpcpro.autotag.owner` | `false` | Auto-equip Owner tag |
| `lpcpro.tag.staff` | `false` | Use Staff tag |
| `lpcpro.tag.helper` | `false` | Use Helper tag |
| `lpcpro.tag.trial-mod` | `false` | Use Trial-Mod tag |
| `lpcpro.tag.mod` | `false` | Use Mod tag |
| `lpcpro.tag.admin` | `false` | Use Admin tag |
| `lpcpro.tag.owner` | `false` | Use Owner tag |

### Games

| Permission | Default | Description |
|---|---|---|
| `lpcpro.game.play` | `true` | Play chat games |
| `lpcpro.game.start` | `op` | Start/stop games |

### Vanish

| Permission | Default | Description |
|---|---|---|
| `lpcpro.vanish.bypass` | `op` | See vanished players in chat |

### Shop

| Permission | Default | Description |
|---|---|---|
| `lpcpro.shop` | — | Access the chat shop |
| `lpcpro.shop.admin` | — | Manage shop currency for players |

### Chat Bubbles

| Permission | Default | Description |
|---|---|---|
| `lpcpro.bubble` | — | Toggle chat bubbles |
| `lpcpro.bubble.admin` | — | Manage chat bubble settings |

### Translation

| Permission | Default | Description |
|---|---|---|
| `lpcpro.translate` | — | Use chat translation |
| `lpcpro.translate.admin` | — | Manage translation settings |

### Macros

| Permission | Default | Description |
|---|---|---|
| `lpcpro.macro` | — | Use and create personal macros |
| `lpcpro.macro.admin` | — | Manage global macros |

### Moderation Queue

| Permission | Default | Description |
|---|---|---|
| `lpcpro.modqueue` | — | View and manage the moderation queue |
| `lpcpro.modqueue.notify` | — | Receive notifications for queued messages |

### Raid Protection

| Permission | Default | Description |
|---|---|---|
| `lpcpro.raidmode` | — | Toggle raid protection mode |
| `lpcpro.raidmode.bypass` | — | Bypass raid mode restrictions |

### Newcomer Management

| Permission | Default | Description |
|---|---|---|
| `lpcpro.newcomer.admin` | — | Manage newcomer status for players |

### Content Filter Bypass

| Permission | Default | Description |
|---|---|---|
| `lpcpro.bypass.filter.sign` | — | Bypass sign content filter |
| `lpcpro.bypass.filter.book` | — | Bypass book content filter |
| `lpcpro.bypass.filter.anvil` | — | Bypass anvil rename filter |

### Additional Declared Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.chatmenu` | `true` | Open recent delivered chat actions on a connected Bedrock client |
| `lpcpro.variable.coords` | `true` | Share a fixed world and block coordinate copy label in local chat |
| `lpcpro.variable.shulker.view` | `true` | View one read-only shulker layer in a snapshot addressed to your session |
| `lpcpro.variable.inv` | `true` | Share a frozen inventory snapshot in local channel chat with [inv]. |
| `lpcpro.variable.ender` | `true` | Share a frozen personal ender chest snapshot with [ender]. |
| `lpcpro.variable.inv.view` | `true` | Open inventory snapshots actually delivered to this session. |
| `lpcpro.variable.ender.view` | `true` | Open ender snapshots actually delivered to this session. |
| `lpcpro.ai.review` | `op` | Review and approve AI word suggestions. |
| `lpcpro.channel.quick` | `true` | Send quick messages to channels. |
| `lpcpro.spy.command` | `op` | Spy on player commands. |
| `lpcpro.chat.reply.public` | `true` | Reply to a recently delivered public message when enabled by the server. |
| `lpcpro.color.black` | `false` | Use black chat color. |
| `lpcpro.color.dark_blue` | `false` | Use dark blue chat color. |
| `lpcpro.color.dark_green` | `false` | Use dark green chat color. |
| `lpcpro.color.dark_aqua` | `false` | Use dark aqua chat color. |
| `lpcpro.color.dark_red` | `false` | Use dark red chat color. |
| `lpcpro.color.dark_purple` | `false` | Use dark purple chat color. |
| `lpcpro.color.gold` | `false` | Use gold chat color. |
| `lpcpro.color.gray` | `false` | Use gray chat color. |
| `lpcpro.color.dark_gray` | `false` | Use dark gray chat color. |
| `lpcpro.color.blue` | `false` | Use blue chat color. |
| `lpcpro.color.green` | `false` | Use green chat color. |
| `lpcpro.color.aqua` | `false` | Use aqua chat color. |
| `lpcpro.color.red` | `false` | Use red chat color. |
| `lpcpro.color.light_purple` | `false` | Use light purple chat color. |
| `lpcpro.color.yellow` | `false` | Use yellow chat color. |
| `lpcpro.color.white` | `false` | Use white chat color. |
| `lpcpro.message.color.hex` | `op` | Use hex colors in chat messages with &#RRGGBB, #RRGGBB, or <#RRGGBB>. |
| `lpcpro.update.notify` | `op` | Receive update notification on join. |
| `lpcpro.channel.deny.speak.*` | `false` | Deny speaking in specific channels. |
| `lpcpro.channel.deny.read.*` | `false` | Declared compatibility node; current channel reading uses membership and the channel's configured access permission |
| `lpcpro.chatprofile` | `true` | Save, privately preview and switch your personal chat style profiles |
| `lpcpro.chatprofile.limit.1` | `false` | Allow creating up to 1 saved chat style profiles |
| `lpcpro.chatprofile.limit.2` | `false` | Allow creating up to 2 saved chat style profiles |
| `lpcpro.chatprofile.limit.3` | `false` | Allow creating up to 3 saved chat style profiles |
| `lpcpro.chatprofile.limit.4` | `false` | Allow creating up to 4 saved chat style profiles |
| `lpcpro.chatprofile.limit.5` | `false` | Allow creating up to 5 saved chat style profiles |
| `lpcpro.chatprofile.limit.6` | `false` | Allow creating up to 6 saved chat style profiles |
| `lpcpro.chatprofile.limit.7` | `false` | Allow creating up to 7 saved chat style profiles |
| `lpcpro.chatprofile.limit.8` | `false` | Allow creating up to 8 saved chat style profiles |
| `lpcpro.chatprofile.limit.9` | `false` | Allow creating up to 9 saved chat style profiles |

### Additional Runtime Permissions

| Permission | Default | Description |
|---|---|---|
| `lpcpro.achievements.admin` | — | Grant/revoke achievements; also needs the base command node |
| `lpcpro.modqueue.admin` | — | Clear or toggle the moderation queue |
| `lpcpro.infractions` | — | View and manage infractions |
| `lpcpro.variable.item` | — | Share the held item with `[item]` or `[i]` |
| `lpcpro.newcomer.bypass` | — | Bypass newcomer restrictions |
| `lpcpro.bypass.antibot` | — | Bypass anti-bot restrictions |
| `lpcpro.bypass.cooldown.partial` | — | Use the configured reduced anti-spam cooldown |
| `lpcpro.emoji.*` / `lpcpro.emoji.<id>` | — | Use permitted built-in emoji replacements |
| `lpcpro.message.color.*` / `lpcpro.message.color.<color>` | — | Type named colors in message text |
| `lpcpro.message.decoration.*` / `lpcpro.message.decoration.<style>` | — | Type message decorations |
| `lpcpro.message.gradient`, `lpcpro.message.rainbow`, `lpcpro.message.transition` | — | Type these color effects in message text |
| `lpcpro.bubble.style.<id>` | — | Match a configured bubble style permission |

Message tag permissions also include `reset`, `click`, `hover`, `keybind`, `translatable`, `insertion`, `font`, `newline`, `selector`, `score`, `nbt`, `pride` and `shadow` under `lpcpro.message.`. Some tags depend on the Adventure API available on the server. Grant interactive or dynamic tags only to trusted players.

The selected-color permissions (`lpcpro.color.*`) and typed-message permissions (`lpcpro.message.*`) serve different purposes. Buying or selecting a color does not grant permission to type arbitrary formatting or click actions.
