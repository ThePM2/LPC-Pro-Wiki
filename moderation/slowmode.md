# 🐢 Slowmode

Slowmode sets a minimum delay between chat messages. It is separate from normal [anti-spam](anti-spam.md), which also checks message similarity.

## Commands

| Command | Description |
|---|---|
| `/slowmode <seconds>` | Set the manual delay |
| `/slowmode off` | Remove the manual delay |
| `/slowmode status` | Show the effective global delay, including an active raid modifier |

The alias is `/slow`. These commands accept an in-game or console sender and require `lpcpro.slowmode`.

```text
/slowmode 5
/slowmode 30s
/slowmode 1m
/slowmode status
/slowmode off
```

Plain numbers are seconds; `s`, `m`, and `h` suffixes are accepted. The maximum is 3,600 seconds; `0` also disables the manual setting. This setting is runtime state rather than a new `slowmode.yml` configuration file.

## Other Delays

Channel, newcomer, normal anti-spam, and raid restrictions can still apply. Raid protection owns a separate delay, so switching raid mode off preserves a manually set slowmode. Reducing the normal anti-spam delay through a shop perk does not remove these other restrictions.

`lpcpro.slowmode.bypass` bypasses the applicable slowmode checks. With proxy announcements configured, a change can be announced to other servers; the announcement does not set their local slowmode value.
