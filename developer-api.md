# Developer API

LPC Pro v2 includes a public API module for third-party plugin developers to integrate with.

{% hint style="warning" %}
The API module (`com.wikmor.lpcpro.api.LPC`) is currently a stub and does not yet expose any methods. It will be populated in a future release. In the meantime, use PlaceholderAPI and Bukkit events to interact with LPC Pro.
{% endhint %}

## API Module

The API is available as a separate module: `lpcpro-api`.

### Maven Dependency

```xml
<dependency>
    <groupId>com.wikmor</groupId>
    <artifactId>lpcpro-api</artifactId>
    <version>1.0.0</version>
    <scope>provided</scope>
</dependency>
```

### Soft Dependency

Add LPC Pro as a soft dependency in your `plugin.yml`:

```yaml
softdepend:
  - LPC-Pro
```

## PlaceholderAPI Integration

The recommended way to read LPC Pro data from another plugin is through PlaceholderAPI:

```java
import me.clip.placeholderapi.PlaceholderAPI;

String messages = PlaceholderAPI.setPlaceholders(player, "%lpcpro_messages%");
String reputation = PlaceholderAPI.setPlaceholders(player, "%lpcpro_reputation%");
String balance = PlaceholderAPI.setPlaceholders(player, "%lpcpro_balance%");
```

See the [Placeholders](placeholders.md) page for the full list of available placeholders.

## Bukkit Events

LPC Pro processes chat through Bukkit's event system. On Paper servers, it uses Paper's `AsyncChatEvent`; on Spigot, it falls back to `AsyncPlayerChatEvent`.

{% hint style="info" %}
LPC Pro listens on **HIGH** priority and **cancels** the event after processing, handling message delivery itself through its channel system. A `MONITOR` listener will see a cancelled event. If you need to read the final result, use PlaceholderAPI or listen on `NORMAL` priority to process before LPC Pro.
{% endhint %}

```java
// Paper (recommended)
@EventHandler(priority = EventPriority.NORMAL)
public void onChat(io.papermc.paper.event.player.AsyncChatEvent event) {
    // LPC Pro processes chat on HIGH priority and cancels the event
    // Listen on NORMAL to process before LPC Pro
}

// Spigot fallback
@EventHandler(priority = EventPriority.NORMAL)
public void onChat(AsyncPlayerChatEvent event) {
    // Same approach for Spigot servers
}
```

## Build Information

| Property | Value |
|---|---|
| Group ID | `com.wikmor` |
| Artifact ID | `lpcpro-api` |
| Version | `1.0.0` |
| Java Target | Java 8 (source/target) |
| Main Package | `com.wikmor.lpcpro.api` |
