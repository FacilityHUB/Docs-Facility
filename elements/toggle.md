# Toggle

A checkbox with an optional keybind, colour pickers and a settings popup.

```lua
local toggle = section:Toggle({
    Text     = "auto farm",
    Flag     = "auto_farm",
    Default  = false,
    Callback = function(state)
        print("auto farm:", state)
    end,
})
```

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Text` | string | `"toggle"` | label |
| `Flag` | string | – | saves the value to configs |
| `Default` | boolean | `false` | starting state |
| `Hint` | string | – | question mark with a tooltip |
| `Style` | string | – | tints the label |
| `Color` | Color3 | – | tints the label, wins over `Style` |
| `Disabled` | boolean | `false` | greyed out and inert |
| `Callback` | function | – | receives the new state |

## Methods

```lua
toggle:Set(true)          -- fires the callback
toggle:Set(true, true)    -- silent, does not fire
toggle:Get()
toggle:SetEnabled(false)
```

## Attachments

Three attachments chain onto a toggle and appear on its row.

### Keybind

```lua
section:Toggle({ Text = "esp", Flag = "esp" })
    :Keybind({ Default = "F", Flag = "esp_key" })
```

Adds a pill on the right of the row. Clicking it listens for a key, right
clicking clears it. The bound key flips the toggle.

The toggle and its keybind appear together in the
[hotkey panel](../hotkey-panel.md).

### Colour picker

```lua
section:Toggle({ Text = "esp box", Flag = "esp_box" })
    :ColorPicker({ Flag = "esp_box_color", Default = Color3.new(1, 0, 0) })
    :ColorPicker({ Flag = "esp_box_fill", Default = Color3.new(0, 0, 0), DefaultAlpha = 0.4 })
```

Adds a swatch on the row. Several can be chained, which suits an outline and a
fill on the same feature.

### Gear

```lua
section:Toggle({ Text = "aimbot", Flag = "aimbot" })
    :Gear(function(panel)
        panel:Slider({ Text = "fov", Min = 10, Max = 400, Default = 120 })
        panel:Dropdown({ Text = "target", Options = { "head", "torso" } })
    end)
```

Adds a small cog that opens a popup holding further elements. Good for settings
that belong to a feature but would clutter the section.

Elements inside a gear behave exactly like elements in a section, flags
included.

## Styling the label

```lua
section:Toggle({ Text = "experimental hitbox", Style = "warning" })
section:Toggle({ Text = "force respawn", Style = "danger" })
```

Marks an option as untested or risky without adding a paragraph. Available
styles: `normal`, `dim`, `bright`, `warning`, `danger`, `success`, `accent`.

A toggle with a custom colour keeps it on hover instead of brightening.
