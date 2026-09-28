# Input

A single line text field.

```lua
section:Input({
    Text        = "prefix",
    Flag        = "prefix",
    Placeholder = "obj_",
    Callback    = function(text, enterPressed)
        print(text, enterPressed)
    end,
})
```

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Text` | string | – | caption above the field |
| `Flag` | string | – | saves the text to configs |
| `Default` | string | `""` | starting text |
| `Placeholder` | string | – | greyed hint when empty |
| `Style` | string | – | tints the caption |
| `Disabled` | boolean | `false` | not editable |
| `Callback` | function | – | receives text and whether Enter was pressed |

The callback fires when the field loses focus or Enter is pressed. The second
argument tells the two apart, which lets you act only on a deliberate submit.

## Methods

```lua
input:Set("value")
input:Get()
input:SetEnabled(false)
```

Long text scrolls inside the field instead of overflowing the card.
