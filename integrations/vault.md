# 🏦 Vault

Vault connects LPC Pro to installed permission/chat and economy providers. Vault alone does not supply an economy or rank data.

## Setup

1. Install Vault and the permission/chat or economy provider you actually need.
2. Restart and check the detected provider in the startup log.
3. For group selection through Vault, use `detection-mode: "VAULT_GROUP"` in `advanced/groups.yml`.

```yaml
detection-mode: "VAULT_GROUP"
```

The provider must expose the relevant Vault service. A missing provider cannot be fixed by adding a placeholder or changing a player's balance in LPC's internal store.

## Shop Economy

`features/shop.yml` can use `currency-mode: "vault"` instead of the default internal `"points"`. Purchases withdraw the exact configured price, preserving a provider's fractional balance.

Uncertain provider transactions are recorded for recovery rather than blindly charged again. See [Chat Shop](../features/chat-shop.md) before resolving a pending purchase. Do not switch currency types as a substitute for migrating balances; the stores are distinct.

On Folia, your chosen economy and commands must themselves support the required scheduling. LPC's Vault adapter does not certify every production provider.

## Placeholders

With PlaceholderAPI's Vault expansion and the relevant provider installed, values such as `%vault_prefix%`, `%vault_suffix%`, `%vault_eco_balance%`, and `%vault_eco_balance_formatted%` can be used. Install the expansion separately; Vault by itself does not register those PAPI values.
