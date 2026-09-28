# Search

A filter field, usually placed above a list you build yourself.

```lua
section:Search({
    Label       = "search",
    Placeholder = "type to filter",
    Live        = true,
    Callback    = function(text)
        rebuildList(text)
    end,
})
```

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Label` | string | – | text on the right of the field |
| `Placeholder` | string | – | greyed hint when empty |
| `Default` | string | `""` | starting text |
| `Live` | boolean | `false` | fire on every keystroke |
| `Flag` | string | – | saves the text to configs |
| `Callback` | function | – | receives the text |

With `Live = false` the callback only fires on Enter or focus loss, which is
better when the filter is expensive.

## Methods

```lua
search:Set("")
search:Get()
```

A [dropdown](dropdown.md) already brings its own search above eight options.
This element is for lists you render yourself, typically into a
[table](table.md).
