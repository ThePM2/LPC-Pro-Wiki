# 🏦 Vault

LPC Pro integrates with [Vault](https://www.spigotmc.org/resources/vault.34315/) for economy and permission abstraction.

## What It Enables

- **Group Detection** — Alternative to LuckPerms for determining player groups
- **Prefixes/Suffixes** — Fetch rank prefixes through Vault's chat API
- **Economy** — Display balance information in chat formats

## Setup

1. Install Vault and an economy plugin (e.g., EssentialsX, CMI) on your server
2. LPC Pro automatically detects Vault

## Group Detection

If you prefer Vault over LuckPerms, set the detection mode in `advanced/groups.yml`:

```yaml
detection-mode: "VAULT_GROUP"
```

## Placeholders

With Vault and PlaceholderAPI installed:

| Placeholder | Description |
|---|---|
| `%vault_prefix%` | Player's prefix via Vault |
| `%vault_suffix%` | Player's suffix via Vault |
| `%vault_eco_balance%` | Player's economy balance |
| `%vault_eco_balance_formatted%` | Formatted balance |
