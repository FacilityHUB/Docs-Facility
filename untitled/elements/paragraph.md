# Paragraph

A titled block of text that wraps, for explaining or warning.

```lua
section:Paragraph({
    Title   = "careful",
    Content = "this option is unstable and may break in some places.",
    Style   = "warning",
    Icon    = "alert-triangle",
})
```

## Options

| Option         | Type   | Default   | Effect                        |
| -------------- | ------ | --------- | ----------------------------- |
| `Title`        | string | –         | heading                       |
| `Content`      | string | –         | body, wraps automatically     |
| `Style`        | string | `normal`  | colours the title             |
| `ContentColor` | Color3 | `TextDim` | body colour                   |
| `Icon`         | string | –         | Lucide icon next to the title |
| `TextSize`     | number | theme     | body size                     |

## Where to put them

In a left or right column a paragraph is about 285 px wide, so a long text wraps over many lines. In a [full width band](../interface/sections.md) it has twice the room and reads far better.

```lua
local notes = Main:Full("notes")

notes:Paragraph({
    Title = "how it works",
    Content = "A band spans both columns. Long explanations belong here.",
    Icon = "info",
})
```

## Side by side

```lua
notes:Split({
    function(left)
        left:Paragraph({ Title = "do", Content = "…", Style = "success" })
    end,
    function(right)
        right:Paragraph({ Title = "avoid", Content = "…", Style = "danger" })
    end,
})
```
