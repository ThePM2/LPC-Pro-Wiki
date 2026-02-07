# ⌨️ Commands & Permissions

Complete reference of all LPC Pro commands and permissions.

## Core Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/lpcpro` | `/lpc` | Main plugin command and help | — |
| `/lpc reload` | — | Reload all configuration files | `lpcpro.command.reload` |
| `/lpc help` | — | Show help menu | — |
| `/lpc admin` | — | Admin commands | `lpcpro.admin` |

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

## Moderation Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/mute <player> [duration] [reason]` | — | Mute a player | `lpcpro.mute` |
| `/mute channel <channel> [duration] [reason]` | — | Mute a channel | `lpcpro.mute.channel` |
| `/mute server [duration] [reason]` | — | Mute entire server chat | `lpcpro.mute.server` |
| `/unmute <player>` | — | Unmute a player | `lpcpro.mute` |
| `/unmute channel <channel>` | — | Unmute a channel | `lpcpro.mute.channel` |
| `/unmute server` | — | Unmute server chat | `lpcpro.mute.server` |
| `/mutes [player]` | — | View mute history (own if no player) | `lpcpro.mute.view` |
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
| `/clearchat [silent] [reason]` | — | Clear the chat (use `silent` to hide staff name) | `lpcpro.clearchat` |
| `/announce <message>` | — | Send a server announcement | `lpcpro.announce` |
| `/slowmode <seconds\|off\|status>` | — | Set, disable, or check slowmode | `lpcpro.slowmode` |
| `/deletemsg <messageId>` | — | Delete a chat message | `lpcpro.chat.delete` |
| `/modqueue` | `/mq`, `/modq` | List pending moderation queue | `lpcpro.modqueue` |
| `/modqueue view <id>` | — | View a specific queued message | `lpcpro.modqueue` |
| `/modqueue approve <id>` | — | Approve a queued message | `lpcpro.modqueue` |
| `/modqueue deny <id>` | — | Deny a queued message | `lpcpro.modqueue` |
| `/modqueue denywarn <id>` | — | Deny and warn the player | `lpcpro.modqueue` |
| `/modqueue clear` | — | Clear all pending messages | `lpcpro.modqueue` |
| `/modqueue toggle` | — | Toggle the moderation queue on/off | `lpcpro.modqueue` |
| `/raidmode [on\|off\|status]` | `/raid`, `/raidprotection` | Toggle or check raid mode | `lpcpro.raidmode` |
| `/raidmode trust <player>` | — | Add player to trusted list | `lpcpro.raidmode` |
| `/raidmode untrust <player>` | — | Remove player from trusted list | `lpcpro.raidmode` |
| `/raidmode trusted` | — | List trusted players | `lpcpro.raidmode` |
| `/newcomer status <player>` | — | Check newcomer status | `lpcpro.newcomer.admin` |
| `/newcomer graduate <player>` | — | Graduate a player from newcomer | `lpcpro.newcomer.admin` |
| `/newcomer reset <player>` | — | Reset player to newcomer status | `lpcpro.newcomer.admin` |
| `/newcomer reload` | — | Reload newcomer configuration | `lpcpro.newcomer.admin` |

## Social Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/rep <player>` | — | Give +1 reputation | `lpcpro.rep.give` |
| `/rep view [player]` | — | View reputation (own if no player) | `lpcpro.rep.view` |
| `/rep top` | — | Reputation leaderboard | `lpcpro.rep.top` |
| `/poll create [duration] <question> \| <options>` | — | Create a poll | `lpcpro.poll.create` |
| `/poll vote <number>` | — | Vote in a poll | `lpcpro.poll.vote` |
| `/poll close` | — | Close a poll | `lpcpro.poll.close` |
| `/achievements` | `/achieve`, `/ach` | Open achievements GUI | `lpcpro.achievements` |
| `/chatgame start [type]` | `/cgame`, `/game` | Start a chat game | `lpcpro.game.start` |
| `/chatgame stats` | — | View game stats | `lpcpro.game.play` |
| `/mail send <player> <message>` | `/email` | Send mail | `lpcpro.mail` |
| `/mail read <id>` | — | Read a specific mail | `lpcpro.mail` |
| `/mail reply <id> <message>` | — | Reply to mail | `lpcpro.mail` |
| `/mail delete <id>` | — | Delete a mail | `lpcpro.mail` |
| `/mail clear` | — | Clear your mail | `lpcpro.mail` |
| `/qr <name>` | — | Send a saved quick reply | `lpcpro.quickreply` |
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

## Customization Commands

| Command | Aliases | Description | Permission |
|---|---|---|---|
| `/color` | — | Open color selection GUI | `lpcpro.color` |
| `/nick <nickname>` | `/nickname`, `/setnick` | Set your nickname | `lpcpro.nick` |
| `/nick off` | — | Remove your nickname | `lpcpro.nick` |
| `/tags` | `/tag`, `/chattags`, `/nametag` | Open tag selection GUI | `lpcpro.tags` |
| `/emoji` | — | View available emojis | `lpcpro.emoji` |
| `/toggle` | — | Toggle chat features | `lpcpro.toggle` |
| `/dnd` | — | Toggle Do Not Disturb | `lpcpro.dnd` |
| `/chatbubble` | `/bubble`, `/bubbles` | Toggle chat bubbles | `lpcpro.bubble` |
| `/translate <text>` | `/tr`, `/trans` | Translate text to your language | `lpcpro.translate` |
| `/translate <lang> <text>` | — | Translate to specific language | `lpcpro.translate` |
| `/translate setlang <code>` | — | Set your default language | `lpcpro.translate` |
| `/macro <name>` | `/macros` | Send a saved macro message | `lpcpro.macro` |
| `/macro list` | — | List all macros | `lpcpro.macro` |
| `/macro set <name> <message>` | — | Create/update a global macro | `lpcpro.macro.admin` |
| `/macro personal <name> <message>` | — | Create a personal macro | `lpcpro.macro` |

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
| `/channelspy [channel]` | `/cspy` | Toggle channel spy | `lpcpro.spy.channel` |
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

## All Permissions

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
| `lpcpro.command.ignore.bypass` | `op` | Cannot be ignored by others |
| `lpcpro.command.unignore` | `true` | Unignore players |
| `lpcpro.dnd` | `true` | Toggle Do Not Disturb |
| `lpcpro.toggle` | `true` | Toggle chat settings |

### Channels

| Permission | Default | Description |
|---|---|---|
| `lpcpro.channel` | `true` | Use channel commands |
| `lpcpro.channel.join.<channel>` | — | Join specific channel |
| `lpcpro.channel.speak.<channel>` | — | Speak in specific channel |

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
| `lpcpro.rep.bypass.cooldown` | `false` | Bypass rep cooldown |
| `lpcpro.poll` | `true` | Base poll permission |
| `lpcpro.poll.create` | `op` | Create polls |
| `lpcpro.poll.vote` | `true` | Vote in polls |
| `lpcpro.poll.close` | `op` | Close polls |
| `lpcpro.mention` | `true` | Mention players |
| `lpcpro.mention.receive` | `true` | Receive mention notifications |
| `lpcpro.mention.everyone` | `op` | Use @everyone and @here |
| `lpcpro.mail` | `true` | Use mail commands |
| `lpcpro.quickreply` | `true` | Use quick reply commands |
| `lpcpro.quickreply.extra` | `false` | Access extra quick reply slots |
| `lpcpro.group` | `true` | View group information |
| `lpcpro.group.admin` | `op` | Manage groups (check player, reload) |

### Customization

| Permission | Default | Description |
|---|---|---|
| `lpcpro.color` | `true` | Open color GUI |
| `lpcpro.color.*` | `op` | All colors |
| `lpcpro.color.hex` | `op` | Hex colors |
| `lpcpro.nick` | `true` | Set nickname |
| `lpcpro.nick.color` | `op` | Colors in nickname |
| `lpcpro.nick.others` | `op` | Set others' nicknames (not yet implemented) |
| `lpcpro.message.*` | `op` | Access to all message formatting tags |
| `lpcpro.message.formatting` | `op` | All formatting codes |
| `lpcpro.emoji` | `true` | View emojis |
| `lpcpro.tags` | `true` | Open tag selection GUI |
| `lpcpro.achievements` | `true` | View achievements GUI |

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
| `lpcpro.translate.bypass` | — | Bypass translation rate limits |

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
