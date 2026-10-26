# 🧑‍💻 Developer API

LPC Pro includes a public channel-aware chat event for third-party plugins. Use it when logging or relaying accepted player chat.

{% hint style="warning" %}
`com.wikmor.lpcpro.api.LPC` is still an empty interface. The usable public API is `LPCChannelChatEvent`; internal manager classes are implementation details and may change.
{% endhint %}

## API Module

The API module is `com.wikmor:lpcpro-api:1.0.0` and is included in the installed LPC Pro JAR. The plugin release is **2.6.0**; the internal API artifact version remains **1.0.0**.

### Maven Dependency

The API is not published to Maven Central. If you have the source checkout, install the module locally:

```bash
mvn -pl lpcpro-api-v2 -am install
```

```xml
<dependency>
    <groupId>com.wikmor</groupId>
    <artifactId>lpcpro-api</artifactId>
    <version>1.0.0</version>
    <scope>provided</scope>
</dependency>
```

Alternatively, place your purchased plugin JAR in `libs/` and save this minimal POM as `libs/lpcpro-local.pom`:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.wikmor</groupId>
    <artifactId>lpcpro-bukkit</artifactId>
    <version>2.6.0</version>
    <packaging>jar</packaging>
</project>
```

Install it with that explicit POM:

```bash
mvn org.apache.maven.plugins:maven-install-plugin:3.1.4:install-file -Dfile=libs/LPC-Pro-2.6.0.jar -DpomFile=libs/lpcpro-local.pom
```

The explicit POM avoids importing the shaded JAR's embedded build POM, which refers to LPC Pro's internal parent/modules. Then use it as a compile-time dependency:

```xml
<dependency>
    <groupId>com.wikmor</groupId>
    <artifactId>lpcpro-bukkit</artifactId>
    <version>2.6.0</version>
    <scope>provided</scope>
</dependency>
```

Compile against your server API as a provided dependency too. Do not shade LPC Pro or its event classes into your plugin.

### Soft Dependency

If your plugin has optional LPC Pro support, declare `softdepend: [LPC-Pro]` and load/register your LPC-specific listener only when LPC Pro is enabled. A plugin that always uses the event should use a hard dependency:

```yaml
name: LpcChatExample
version: 1.0.0
main: example.lpc.LpcChatExample
api-version: '1.16'
depend: [LPC-Pro]
```

## Bukkit Events

LPC Pro consumes and cancels the vanilla Paper `AsyncChatEvent` or Spigot `AsyncPlayerChatEvent` before its own delivery. A listener before LPC Pro sees input without final channel context; a later listener sees a cancelled event. Use `com.wikmor.lpcpro.api.event.LPCChannelChatEvent` for the processed result.

| Method | Description |
|---|---|
| `getPlayer()` | The sending player |
| `getChannelId()` | Channel ID from `chat/channels.yml` |
| `getChannelDisplayName()` | Configured display name, possibly `null` |
| `isChannelRestricted()` | Whether the channel defines an access permission |
| `isAudienceRestricted()` | Whether the channel is restricted or the upstream event narrowed the audience |
| `getMessage()` | Final processed message string, before per-recipient format rendering |
| `getRecipients()` | Immutable snapshot of successful send calls, or scheduled candidates when delivery is pending |
| `isDeliveryComplete()` | `false` for scheduled Folia delivery; `true` after direct delivery calls complete |

{% hint style="info" %}
The event is notification-only and cannot cancel a message. It fires once per accepted ordinary outbound player channel message after delivery has been attempted or scheduled. Incoming Discord and proxy messages, and contextual public replies, do not fire it. A completed send call does not prove that a Minecraft client displayed the message.
{% endhint %}

### Example Listener

This complete example logs unrestricted, completed chat deliveries. A relay should apply the same privacy checks before sending anything outside the server:

```java
package example.lpc;

import com.wikmor.lpcpro.api.event.LPCChannelChatEvent;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.plugin.java.JavaPlugin;

public final class LpcChatExample extends JavaPlugin implements Listener {
    @Override
    public void onEnable() {
        getServer().getPluginManager().registerEvents(this, this);
    }

    @EventHandler
    public void onChannelChat(LPCChannelChatEvent event) {
        if (event.isChannelRestricted() || event.isAudienceRestricted()) return;
        if (!event.isDeliveryComplete() || event.getRecipients().isEmpty()) return;

        String line = "[" + event.getChannelId() + "] "
                + event.getPlayer().getName() + ": " + event.getMessage();
        getLogger().info(line);
    }
}
```

The `isDeliveryComplete()` guard intentionally skips pending Folia deliveries. If you need those messages, implement a policy for scheduled candidates instead of treating them as confirmed recipients.

### Threading and Privacy

- Check `event.isAsynchronous()`. Processing is moved to the sender's owning context: the main thread on ordinary Paper/Spigot, or the sender's region on Folia.
- A synchronous event flag does not grant ownership of another player's Folia region. Schedule entity access on the appropriate owning context.
- Do not perform blocking HTTP requests in the listener. Capture immutable values and queue external I/O separately.
- Check `isAudienceRestricted()`, not just a hardcoded `staff` channel name. Upstream plugins can narrow an otherwise public channel's viewers.
- The recipient set is not a client receipt, and the event is not a hook for suppressing or rewriting chat.

## PlaceholderAPI Integration

Use PlaceholderAPI to read LPC Pro data from another plugin. Compile with PlaceholderAPI as a provided dependency and declare it in your dependencies if your code always calls it.

```java
package example.lpc;

import me.clip.placeholderapi.PlaceholderAPI;
import org.bukkit.entity.Player;

public final class LpcPlaceholderExample {
    public String summary(Player player) {
        return PlaceholderAPI.setPlaceholders(player,
                "Messages: %lpcpro_messages% | Reputation: %lpcpro_reputation%"
                        + " | Balance: %lpcpro_balance%");
    }
}
```

Call player-related expansions on the player's owning context. See [Placeholders](placeholders.md) for the full list and unavailable/offline values.

## Achievement Integrations

Quest plugins, Skript or console-capable integrations can dispatch:

```text
achievements grant Steve chatterbox
achievements revoke Steve chatterbox
```

`grant` needs an online player, persists the unlock, announces it and runs configured reward commands. Repeating a grant for an already unlocked achievement does not run its rewards again. `revoke` also accepts a known offline player and removes the saved unlock; it does not undo rewards already issued. Players need both `lpcpro.achievements` and `lpcpro.achievements.admin`. See [Achievements](features/achievements.md).

## Build Information

| Property | Value |
|---|---|
| Group ID | `com.wikmor` |
| API Artifact ID | `lpcpro-api` |
| API Version | `1.0.0` |
| Plugin Version | `2.6.0` |
| Java Target | Java 16 bytecode; use the Java version required by your server |
| Main Package | `com.wikmor.lpcpro.api` |
