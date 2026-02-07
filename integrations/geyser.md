# Geyser & Floodgate

LPC Pro integrates with [Geyser](https://geysermc.org/) and [Floodgate](https://wiki.geysermc.org/floodgate/) to detect Bedrock players and adapt the chat experience accordingly.

## What It Enables

- **Bedrock Player Detection** — Identify players connecting from Bedrock Edition
- **Bedrock Username Retrieval** — Get the player's Bedrock gamertag
- **Device Type Detection** — Detect which device a Bedrock player is using

## Setup

1. Install Geyser-Spigot and Floodgate on your server
2. Ensure `geyser: true` is set in `config.yml` under `hooks:`

## How It Works

LPC Pro uses the Floodgate API to detect Bedrock players. When a Bedrock player is detected:

- Their Bedrock gamertag can be used in chat formatting
- Device-specific behavior can be applied
- Chat formatting can be adapted for Bedrock clients

{% hint style="info" %}
Both **Geyser-Spigot** and **Floodgate** must be installed. Floodgate provides the API that LPC Pro uses for detection.
{% endhint %}
