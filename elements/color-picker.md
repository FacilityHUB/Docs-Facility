# Color picker

A colour swatch opening a picker with hue, saturation, value, an optional alpha
bar and a hex field.

```lua
section:ColorPicker({
    Text     = "highlight",
    Flag     = "highlight",
    Default  = Color3.fromRGB(232, 161, 168),
    Callback = function(color, alpha)
        print(color, alpha)
    end,
})
```

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Text` | string | `"color"` | label |
| `Flag` | string | – | saves the colour to configs |
| `Default` | Color3 | white | starting colour |
| `DefaultAlpha` | number | `1` | starting alpha |
| `Alpha` | boolean | `true` | show the alpha bar |
| `Style` | string | – | tints the label |
| `Disabled` | boolean | `false` | greyed out and inert |
| `Callback` | function | – | receives colour and alpha |

## Methods

```lua
picker:Set(Color3.fromRGB(0, 255, 0))
picker:Set(Color3.new(1, 0, 0), 0.5)
picker:Set(color, alpha, true)   -- silent
picker:Get()                     -- returns colour, alpha
```

## Hex

The picker holds a hex field. It accepts `#RRGGBB` and `#RRGGBBAA`, and shows
the current value in that form, which makes a colour easy to copy between
scripts.

## On a toggle

Chained onto a toggle, the swatch sits on its row:

```lua
section:Toggle({ Text = "esp box", Flag = "esp_box" })
    :ColorPicker({ Flag = "box_outline", Default = Color3.new(1, 0, 0) })
    :ColorPicker({ Flag = "box_fill", DefaultAlpha = 0.3 })
```

Two pickers on one row is the usual pattern for an outline and its fill.
