# Installation

## Step 1: Download

Download the latest `lpcpro-bukkit-v2-X.X.X.jar` file.

## Step 2: Install the Plugin

1. Stop your server.
2. Place the `.jar` file into your server's `plugins/` folder.
3. Start the server.

LPC Pro will generate its configuration files on first startup:

```
plugins/LPC-Pro/
├── config.yml                          # Main settings
├── database.yml                        # Database connection
├── translation.yml                     # Chat translation
├── chat/
│   ├── channels.yml                    # Chat channels
│   ├── colors.yml                      # Color settings
│   ├── emojis.yml                      # Emoji settings
│   ├── grammar.yml                     # Grammar correction
│   ├── bubbles.yml                     # Chat bubbles
│   ├── mentions.yml                    # @mention settings
│   └── tags.yml                        # Chat tags
├── moderation/
│   ├── moderation.yml                  # Filter settings (spam, caps, ads, swear)
│   ├── content-filter.yml              # Content filter (signs/books/anvil)
│   ├── ai-filter.yml                   # AI content moderation
│   ├── cloud-filter.yml                # Cloud-based filter
│   ├── console-filter.yml              # Console output filter
│   ├── antibot.yml                     # Anti-bot protection
│   ├── raidprotection.yml              # Raid protection
│   └── reports.yml                     # Report system
├── features/
│   ├── achievements.yml                # Chat achievements
│   ├── games.yml                       # Chat games
│   ├── mail.yml                        # Mail system
│   ├── macros.yml                      # Chat macros
│   ├── motd.yml                        # MOTD settings
│   ├── newcomer.yml                    # New player handling
│   ├── offlinemessages.yml             # Offline message settings
│   ├── polls.yml                       # Polls
│   ├── quickreply.yml                  # Quick reply shortcuts
│   ├── reputation.yml                  # Rep system
│   ├── servermessages.yml              # Join/quit/death messages
│   ├── shop.yml                        # Chat shop / cosmetics
│   ├── smart-announcements.yml         # Context-aware announcements
│   ├── tablist.yml                     # Tab list header/footer
│   └── custom-commands.yml             # Custom commands
├── integration/
│   ├── discord.yml                     # Discord integration
│   ├── proxy.yml                       # Proxy/network settings
│   └── server-links.yml                # Server links
├── advanced/
│   ├── groups.yml                      # Rank-based settings
│   ├── variables.yml                   # Custom variables
│   ├── command-settings.yml            # Command settings
│   ├── message-interceptor.yml         # Message interception
│   └── message-deletion.yml            # Message deletion
└── formats/                            # Chat format templates
    ├── chat.yml
    ├── msg-sender.yml
    ├── msg-receiver.yml
    ├── staff-chat.yml
    └── groups/                         # Group-specific formats
```

## Step 3: Install Optional Plugins

Install any optional dependencies you want to use (see [Requirements](requirements.md)). LPC Pro automatically detects installed plugins and enables their integrations.

## Step 4: Configure

Edit the generated configuration files to match your server's needs. See the [Configuration](../configuration/main-config.md) section for details.

## Step 5: Reload

After editing configuration files, use `/lpc reload` to apply changes without restarting the server.

{% hint style="warning" %}
The `database.yml` file does **not** support reloading. Changes to database settings require a full server restart.
{% endhint %}
