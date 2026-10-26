# 📍 Coordinate Sharing

Type `[coords]` in local channel chat to share the world name and current block coordinates. The delivered label can copy the location to the recipient's clipboard on clients that support the action.

## Usage

```text
Meet me here: [coords]
```

For example, the label can appear as `[world: 120, 64, -250]`. Clicking copies:

```text
world: 120 64 -250
```

This is a fixed location captured for that message. It does not track the player, create a waypoint or run a teleport command. Negative positions use block coordinates, as Minecraft does, rather than rounding toward zero.

Only share a location when you want that chat audience to know it. Normal channel access and message delivery rules still apply.

## Configuration

In `plugins/LPC-Pro/advanced/variables.yml`:

```yaml
coords-variable:
  enabled: true
  max-uses-per-message: 3
```

`max-uses-per-message` accepts values from `1` to `4`. All replacements in one accepted message use the same captured location. If the token count exceeds the limit, coordinate replacements are skipped and the sender receives a notice.

Use `/lpc reload` after editing. The feature is independent of inventory sharing, so disabling `[inv]` does not disable `[coords]`.

## Permission

| Permission | Default | Description |
|---|---|---|
| `lpcpro.variable.coords` | `true` | Share `[coords]` in local chat |

The token must be in the player's original message. A trusted message rewrite cannot add extra coordinate actions on the player's behalf.

## Client Support

The label remains readable even if a client cannot use the clipboard action. Clipboard behavior depends on the Minecraft client and platform; native Bedrock chat does not provide the same Java click interaction. No teleport or clipboard fallback is added to `/chatmenu`.

This feature is intended for the local channel message body, not private messages, mail or a cross-server location service. It uses the actual world name, with no automatic world alias or dimension conversion.
