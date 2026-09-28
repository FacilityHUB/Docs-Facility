# Slider

A numeric value on a rail, with an editable field.

```lua
local slider = section:Slider({
    Text     = "walk speed",
    Flag     = "walk_speed",
    Min      = 16,
    Max      = 200,
    Default  = 16,
    Callback = function(value)
        local humanoid = game.Players.LocalPlayer.Character
            and game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
        if humanoid then humanoid.WalkSpeed = value end
    end,
})
```

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Text` | string | `"slider"` | label |
| `Flag` | string | – | saves the value to configs |
| `Min` | number | `0` | lower bound |
| `Max` | number | `100` | upper bound |
| `Default` | number | `Min` | starting value |
| `Step` | number | `1` | increment |
| `Decimals` | number | `0` | digits shown |
| `Suffix` | string | – | appended to the value, e.g. `" studs"` |
| `ZeroText` | string | – | shown instead of `0` |
| `Style` | string | – | tints the label |
| `Disabled` | boolean | `false` | greyed out and inert |
| `Callback` | function | – | receives the value |

## Typing a value

The number on the right is a text field. Click it, type, press Enter. The value
is clamped to the range, and an invalid entry restores the previous one.

Dragging is fine for a narrow range, typing is faster for something like `0` to
`9999`.

## Methods

```lua
slider:Set(64)
slider:Set(64, true)   -- silent
slider:Get()
slider:SetEnabled(false)
```

## Decimals and steps

```lua
section:Slider({
    Text = "smoothing",
    Min = 0, Max = 1,
    Step = 0.05,
    Decimals = 2,
    Default = 0.35,
})
```

`Step` controls the movement, `Decimals` only the display. A step of `0.05` with
zero decimals shows a value jumping between whole numbers, which looks broken;
keep them consistent.

## Zero as a special case

```lua
section:Slider({
    Text = "max distance",
    Min = 0, Max = 5000,
    Default = 0,
    ZeroText = "unlimited",
})
```

Common when zero means off rather than the smallest value.
