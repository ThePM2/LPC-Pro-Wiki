# ViaVersion

LPC Pro integrates with [ViaVersion](https://www.spigotmc.org/resources/viaversion.19254/) to detect which Minecraft client version each player is using.

## What It Enables

- **Client Version Detection** — Know which Minecraft version each player is connecting with
- **Version-Specific Behavior** — Adapt features based on the player's client version

## Setup

1. Install ViaVersion on your server
2. Ensure `via-version: true` is set in `config.yml` under `hooks:`

## How It Works

ViaVersion allows players on different Minecraft versions to connect to your server. LPC Pro reads the client's protocol version through ViaVersion's API and can adapt behavior accordingly.

This is primarily used internally by LPC Pro to ensure compatibility across different client versions.
