# Dropdown

A list of options, single or multiple selection, with automatic search.

```lua
local dropdown = section:Dropdown({
    Text     = "target part",
    Flag     = "target_part",
    Options  = { "head", "torso", "root" },
    Default  = "head",
    Callback = function(value)
        print("target:", value)
    end,
})
```

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Text` | string | – | caption above the field |
| `Flag` | string | – | saves the value to configs |
| `Options` | table | `{}` | the entries |
| `Default` | string/table | – | starting selection |
| `Multi` | boolean | `false` | allow several selections |
| `Empty` | string | `"none"` | label when nothing is selected |
| `Search` | boolean | auto | forced on above 8 options |
| `MaxHeight` | number | `180` | list height before scrolling |
| `Style` | string | – | tints the caption |
| `Disabled` | boolean | `false` | greyed out and inert |
| `Callback` | function | – | receives the selection |

## Multiple selection

```lua
section:Dropdown({
    Text    = "ignore",
    Flag    = "ignore_list",
    Options = { "friends", "team", "npc" },
    Multi   = true,
    Default = { "friends" },
    Empty   = "nobody",
    Callback = function(selected)
        -- selected is a table
    end,
})
```

With `Multi`, the field shows the selection comma separated and the callback
receives a table.

## Search

Above eight options a search field appears at the top of the list. Set
`Search = true` to force it, `false` to keep it off.

That is what makes a dropdown suitable for long lists: fifty entries stay usable
where a radio group would not.

## Methods

```lua
dropdown:Set("torso")
dropdown:Set({ "friends", "team" })   -- multi
dropdown:Get()
dropdown:SetOptions({ "a", "b", "c" })   -- rebuilds the list
dropdown:SetEnabled(false)
```

`SetOptions` keeps the current selection when the value still exists in the new
list.

## Inside a panel

Dropdowns work in [floating panels](../panels.md). The list opens in the panel's
own popup layer, so it works with the main interface closed.
