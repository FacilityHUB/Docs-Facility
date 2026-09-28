# Button

```lua
section:Button({
    Text     = "reload",
    Callback = function()
        Library:Notify("facility", "reloaded.", 3)
    end,
})
```

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Text` | string | `"button"` | label |
| `Style` | string | – | tints the label |
| `Color` | Color3 | – | tints the label, wins over `Style` |
| `Disabled` | boolean | `false` | greyed out and inert |
| `Callback` | function | – | runs on click |

## Rows

```lua
section:ButtonRow({
    { Text = "start", Callback = function() end },
    { Text = "stop",  Callback = function() end },
})
```

Buttons share the width evenly. Two or three per row stay readable, beyond that
the labels get cramped.

## Dangerous actions

```lua
section:Button({
    Text = "reset everything",
    Style = "danger",
    Callback = function()
        Window:Confirm({
            Title = "reset",
            Text = "This clears every setting. Continue?",
            Confirm = "reset",
            Cancel = "cancel",
            OnConfirm = function() Library:ResetDefaults() end,
        })
    end,
})
```

Pair a red label with a [confirmation](../dialogs.md) for anything destructive.

## Methods

```lua
button:SetEnabled(false)
```
