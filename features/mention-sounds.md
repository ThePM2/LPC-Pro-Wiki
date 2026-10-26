# 🔔 Mention Sounds

Players can choose a personal mention tone without changing the server's sound for everybody. The selection is stored with their player settings.

## Choices

| Choice | Behavior |
|---|---|
| `default` | Use the current server mention sound |
| `chime` | Note-block chime |
| `bell` | Note-block bell |
| `silent` | No mention sound; eligible highlights and titles remain |

Old stored sound strings use the server-default choice until a supported personal selection is made. Personal tones do not bypass the server's disabled mention-sound setting.

## Commands

```text
/toggle mention-sound
/toggle mention-sound preview chime
/toggle mention-sound chime
```

The first command shows the current choice. `preview` auditions a choice privately without saving it; omit `preview` to select it. Replace `chime` with `default`, `bell` or `silent` as needed.

| Command | Description |
|---|---|
| `/toggle mention-sound <choice>` | Save a personal tone |
| `/toggle mention-sound preview <choice>` | Private audition; leave the choice unchanged |
| `/toggle gui` | Open the mention-sound inventory menu |
| `/toggle menu` | Open chat settings, including the mention-sound section |

The command requires `lpcpro.toggle`, allowed by default. The mention feature and loaded player settings must be available. Auditioning `silent` produces no sound; when the server disables mention sounds, an audition does not override it.

## Server Configuration

The server default remains in `plugins/LPC-Pro/chat/mentions.yml`:

```yaml
sound:
  enabled: true
  name: "entity.experience_orb.pickup"
  volume: 1.0
  pitch: 1.0
```

Personal chime and bell choices use the configured volume and pitch. Setting `sound.enabled: false` silences all mention tones. The main `config.yml` switch `enable-mentions` and `chat/mentions.yml` master `enabled` must also allow mention processing.

## Related Settings

`/toggle mentions` controls receiving mention effects. Choosing `silent` changes only the tone and keeps highlighting and titles for an otherwise eligible mention.

`/toggle sounds` controls ordinary chat and private-message notifications. It is separate from the personal mention tone. See [Mentions](mentions.md) for audience rules and [Personal Chat Settings](chat-settings.md) for the other receiving preferences.

The native Bedrock settings route is `/toggle menu` when a genuine current forms connection is available. `/toggle gui` retains its separate inventory menu. Actual sound output also depends on the client's audio settings.
