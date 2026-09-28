# Notifications

```lua
Library:Notify({
    Title    = "facility",
    Text     = "script loaded",
    Duration = 4,
    Style    = "success",
    Icon     = "check",
})
```

## Shorthands

```lua
Library:Notify("facility", "loaded", 4)

Library:Warn("careful", "this is experimental", 4)
Library:Error("failed", "could not reach the server", 6)
Library:Success("done", "config applied", 3)
```

Each shorthand picks its own style and icon.

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Title` | string | – | heading |
| `Text` | string | – | body |
| `Duration` | number | `4` | seconds on screen |
| `Style` | string | `normal` | `normal`, `warning`, `danger`, `success` |
| `Color` | Color3 | – | explicit accent bar colour |
| `Icon` | string | – | overrides the style's icon |

## Behaviour

They slide in from the right and stack upward. Five at most; beyond that the
oldest is removed to make room.

```lua
Library.NotificationsEnabled = false   -- silence everything
Library.NotificationLimit = 3
```

Notifications live in their own `ScreenGui`, so they appear whether the
interface is open or not.

## Errors in callbacks

A callback that errors produces a red notification naming the element
responsible, plus the full trace in the console. Nothing fails silently.
