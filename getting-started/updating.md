# 🔄 Updating & Recovery

Keep a recoverable copy before updating LPC Pro. Updating should retain your custom formats, translations, player settings, and durable records.

## Before Updating

1. Stop the server normally so accepted storage work can finish.
2. Back up the current LPC Pro JAR and the **entire** `plugins/LPC-Pro/` directory, including hidden migration markers, data, and style-editor backups.
3. Back up the database separately. For SQLite, copy it while the server is stopped; for MySQL, take a consistent database backup.
4. Test the new JAR against a separate copy of that state.

Replace the old JAR with the new one while stopped, keep a single LPC Pro JAR in `plugins/`, then start the server. Read startup/migration messages and check `/lpc status` before inviting players back.

## Configuration Migration

Current files use `chat/`, `moderation/`, `features/`, `integration/`, and `advanced/` subdirectories. Older root-level files are migrated where supported. When old and organized files conflict, the organized file is authoritative and conflicting source files are preserved for you to review. Do not delete a custom file just because another copy exists.

Existing owner settings remain authoritative. New receiving preferences receive by default. Public replies and AI remain opt-in; updating does not mean either service is ready to use. Known retired default AI profiles have a guarded migration, while customized provider/model/endpoint selections are preserved. See [AI Filter](../moderation/ai-filter.md).

After file edits, `/lpc reload` applies supported changes. All top-level `enable...` switches in `config.yml` and database connection settings require restart.

## First-Install Import

A genuinely new LPC Pro installation can import supported **EssentialsChat** layouts. It is a conservative first-run import, not a migration of all Essentials data or the free LPC plugin. Existing LPC Pro settings take precedence. Unsupported layouts are reported instead of guessed.

The importer keeps source and target recovery information under the onboarding area. Review the startup report and use `/lpc diagnose` to confirm the format in use. Removing the data directory to trigger an import also removes your settings and is not an update procedure.

## Proxy Networks

Update authenticated proxy peers together. Older unauthenticated peers are incompatible with the current wire protocol. Configure a distinct local server ID/key and the trusted remote IDs/keys on each backend, then verify a message with the intended audience. A shared MySQL database does not replace transport or synchronize every online cache. See [Proxy / Network](../integrations/proxy.md).

## Check After Startup

- Send ordinary chat with an account that has normal player permissions.
- Check the selected format, channel access, private messages, and saved personal settings.
- Open a shared inventory and reload; old snapshot menus should close safely.
- Check custom messages and the enabled integrations you actually use.
- Check the log for database/schema, library, or reload failures.

The 2.6.0 existing-data release check covered a private test fixture. Test your own previous release and configuration before replacing a live server.

## Restore a Previous Version

Stop the server and restore the **matching JAR, plugin directory, and database backup together**. Replacing only the JAR does not undo database or configuration migrations. Keep the failed upgrade copy for diagnosis.

To undo only a saved editor layout, use `/lpc style restore` for the selected loaded format. That restores the matching predecessor; it is not a full plugin rollback. External edits are protected from an unexpected overwrite.

## Purchase Recovery

An interrupted Vault purchase may require an administrator to confirm the provider's ledger before using `/chatshop recover <player> <item-id> paid` or `not-paid`. Do not blindly retry or delete unresolved operations. See [Chat Shop](../features/chat-shop.md).
