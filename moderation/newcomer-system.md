# 🆕 Newcomer System

The optional newcomer system gives new players a badge, an additional chat delay, and a limit on mention recipients. Configuration is in `features/newcomer.yml`; it is disabled by default.

## Configuration

```yaml
enabled: false
required-playtime-minutes: 60
required-message-count: 10
newcomer-tag: "<gray>[New]</gray>"
show-welcome-message: false
welcome-messages: []
apply-slowmode: true
newcomer-slowmode-seconds: 5
mention-restriction: false
max-mentions-per-message: 1
```

## How It Works

A player graduates when **either** requirement is met: 60 tracked minutes or ten accepted normal chat messages by default. A zero requirement allows immediate graduation. Playtime is connected time tracked by LPC Pro, not a lifetime Minecraft statistic.

State persists between sessions. While state is loading or unavailable, newcomer chat is paused instead of guessing that the player is unrestricted. Check `/lpc status` and repair storage problems before asking the player to reconnect.

## Features

### Newcomer Tag

The badge is added alongside the player's existing rank/selected tag. It does not replace them. The main `enable-tags` setting still controls tag rendering.

### Welcome Messages

To add a welcome, enable `show-welcome-message` and fill the list:

```yaml
show-welcome-message: true
welcome-messages:
  - "<green>Welcome to the server, <white>{player}</white>!"
```

This is an optional example, not the default message list.

### Slowmode

`apply-slowmode: true` adds the configured five-second newcomer floor. Normal anti-spam and other delays can still apply. `lpcpro.slowmode.bypass` skips the delay but does not grant the full newcomer bypass.

### Mention Restrictions

When `mention-restriction: true`, `max-mentions-per-message` limits unique eligible recipients. This also limits expanded mentions such as `@everyone`. Use `0` to allow no recipients or `-1` for no newcomer cap. A message that exceeds the cap is rejected before mention notifications are sent.

## Commands

| Command | Description |
|---|---|
| `/newcomer status <player>` | Inspect a known player's newcomer state |
| `/newcomer graduate <player>` | Graduate the player manually |
| `/newcomer reset <player>` | Reset newcomer progress |
| `/newcomer reload` | Reload the newcomer policy |

These in-game staff commands require `lpcpro.newcomer.admin`; aliases are `/newbie` and `/nc`. Invalid reloads keep the last valid newcomer configuration.

## Permissions

| Permission | Description |
|---|---|
| `lpcpro.newcomer.admin` | Use newcomer administration commands |
| `lpcpro.newcomer.bypass` | Skip the badge, restrictions, and newcomer progress increments |
| `lpcpro.slowmode.bypass` | Skip the applicable delay only |

Use `/lpc diagnose <online-player>` to inspect the currently cached newcomer policy alongside the player's chat route.
