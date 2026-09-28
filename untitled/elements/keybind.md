# Keybind

A key binding, standalone or attached to a toggle.

```lua
section:Keybind({
    Text     = "hold to inspect",
    Flag     = "inspect_key",
    Default  = "E",
    Mode     = "hold",
    Callback = function(down)
        print("held:", down)
    end,
})
```

## Options

| Option      | Type     | Default     | Effect                            |
| ----------- | -------- | ----------- | --------------------------------- |
| `Text`      | string   | `"keybind"` | label                             |
| `Flag`      | string   | –           | saves the key to configs          |
| `Default`   | string   | –           | starting key                      |
| `Mode`      | string   | `"press"`   | `"press"`, `"hold"` or `"toggle"` |
| `Style`     | string   | –           | tints the label                   |
| `Disabled`  | boolean  | `false`     | ignores the key entirely          |
| `Callback`  | function | –           | receives the state                |
| `OnChanged` | function | –           | receives the new key when rebound |

## Modes

**`press` and `hold`** are the same thing: the callback receives `true` when the key goes down and `false` when it is released.

**`toggle`** flips an internal state on each press and passes that state to the callback. The current value is readable on `keybind.Active`.

```lua
section:Keybind({
    Text = "auto collect",
    Flag = "collect_key",
    Default = "H",
    Mode = "toggle",
    Callback = function(active)
        collecting = active
    end,
})
```

## Binding

Click the pill to listen, then press any key. Right click clears it. `MB1` to `MB5` cover mouse buttons.

## In the hotkey panel

Behaviour differs by mode, see [Hotkey panel](../features/hotkey-panel.md):

| Mode             | Shown                                     |
| ---------------- | ----------------------------------------- |
| `press` / `hold` | only while the key is held                |
| `toggle`         | always, accent when active, grey when not |

## Methods

```lua
keybind:Set("F")
keybind:Get()        -- the key as a string
keybind:SetEnabled(false)
keybind.Active       -- toggle mode only
```

A disabled keybind ignores its key, not just its pill.
