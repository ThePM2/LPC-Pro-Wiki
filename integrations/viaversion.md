# 🔀 ViaVersion

LPC Pro can read a connected Java client's protocol number through ViaVersion. The ViaVersion hook is optional; it does not change the Minecraft server version running LPC.

## Setup

1. Install a ViaVersion version appropriate for your server and clients.
2. Keep this setting in `config.yml`:

```yaml
hooks:
  via-version: true
```

3. Restart after installing the provider and check its own connection compatibility.

## How It Works

LPC reads the player's protocol from ViaVersion's API. A missing/unavailable result is treated as unknown. This information can help internal client capability checks; it does not guarantee that a newer client receives every feature of a newer server.

ViaVersion does not replace Geyser for Bedrock connections, provide a resource pack, or certify LPC on every translated version. Match your server, client, ViaVersion, and optional provider versions when checking a problem.
