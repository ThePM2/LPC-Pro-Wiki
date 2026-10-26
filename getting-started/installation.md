# 💾 Installation

## Step 1: Download

Download your LPC Pro release JAR, for example `LPC-Pro-2.6.0.jar`. Keep one LPC Pro JAR in the server's `plugins/` directory.

## Step 2: Install the Plugin

1. Stop the server.
2. Place the release JAR in `plugins/`.
3. Install any optional providers you need, using versions compatible with your server.
4. Start the server and check the LPC Pro startup log.

Runtime libraries may need to be downloaded on first startup. If startup fails, resolve the reported library or database error before continuing; a JAR being present is not proof that initialization succeeded.

LPC Pro organizes its files under `plugins/LPC-Pro/`:

```text
plugins/LPC-Pro/
├── config.yml                         # Main switches and hooks
├── database.yml                       # Storage connection
├── translation.yml                    # Requested text translation
├── messages.json                      # Player-facing text
├── chat/                              # channels, colors, emojis, grammar,
│                                      # bubbles, mentions, tags, sounds,
│                                      # settings, public-replies
├── moderation/                        # moderation, AI/cloud/content filters,
│                                      # console filter, anti-bot, raids, reports
├── features/                          # games, shop, guis, mail, offline messages,
│                                      # profiles' supporting cosmetics, newcomer,
│                                      # MOTD, tablist, polls, reputation,
│                                      # achievements, logging and announcements
├── integration/                       # discord.yml, proxy.yml, server-links.yml
├── advanced/                          # groups, variables, command settings/spy,
│                                      # interception and deletion settings
├── formats/                           # chat.yml, msg-sender.yml,
│   └── groups/                        # msg-receiver.yml, staff-chat.yml, ranks
├── data/                              # Feature-owned durable records
├── cache/                             # Bounded identity/provider caches
└── style-editor/backups/               # Previous saved format bytes
```

The comments abbreviate file names: for example channels are in `chat/channels.yml`, the shop is in `features/shop.yml`, and variables are in `advanced/variables.yml`. Some files are created by their feature manager. Use the path on each feature page rather than creating a second root-level copy.

## Step 3: Check the Installation

As an administrator, run:

```text
/lpc info
/lpc status
/lpc diagnose
```

`/lpc` requires `lpcpro.admin`. Diagnostics explain the selected channel and format without broadcasting a test message. A feature can be initialized while its own optional `enabled` setting remains off.

## Step 4: Configure

Follow [Initial Setup](initial-setup.md) for your first visible chat style. Keep only one plugin responsible for formatting the same public chat event. On a genuinely new LPC Pro installation, supported EssentialsChat layouts may be imported automatically with a backup; see [Updating & Recovery](updating.md#first-install-import).

## Step 5: Apply Changes

Use `/lpc reload` for supported file changes and check its response and `/lpc status` afterward.

{% hint style="warning" %}
Changing any top-level `enable...` switch in `config.yml`, or the database connection, requires a full server restart. Reload keeps the running feature switches until then. Replace a plugin JAR with the server stopped; do not use a general-purpose plugin hot-loader.
{% endhint %}

Already using LPC Pro? Follow [Updating & Recovery](updating.md) before replacing it.
