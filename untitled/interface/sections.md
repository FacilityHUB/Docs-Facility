# Sections

A section is a card inside a tab. Every element goes into one.

```lua
local section = Main:Section("global", 1)
```

The second argument picks the column: `1` for the left, `2` for the right,
`"full"` for a band spanning both. Omitted, it defaults to the left column.

## Layout

Columns are created on demand. A full width section closes the current pair, so
sections declared after it start a new row below:

```lua
Main:Section("global", 1)     -- row 1, left
Main:Section("settings", 2)   -- row 1, right
Main:Full("notes")            -- full width band
Main:Section("advanced", 1)   -- row 2, left
Main:Section("misc", 2)       -- row 2, right
```

`Main:Full(title)` and `Main:Section(title, "full")` are the same thing.

A left column section is about 285 px wide, a full width band twice that. Long
paragraphs and tables with several columns read much better in a band.

## Collapsing

Every section collapses when its header is clicked, and the chevron rotates.
Nothing to declare, it works out of the box.

## Title style

```lua
local Window = Library:Window({
    SectionTitleStyle = "border",   -- "inline" is the default
})
```

**inline** puts the title inside the card, above the first element.

**border** places it across the top border, cutting the stroke behind the text.
It is set once for the whole interface.

## Splitting inside a section

`Split` places two or three sub containers side by side. Useful in a full width
band, or to pair two short lists.

```lua
local notes = Main:Full("reference")

notes:Split({
    function(left)
        left:Paragraph({
            Title = "careful",
            Content = "options with a gear expose extra settings.",
            Style = "warning",
        })
    end,
    function(right)
        right:Paragraph({
            Title = "configs",
            Content = "only flagged elements are saved.",
            Style = "success",
        })
    end,
})
```

Each sub container exposes the full element API, not just text. Toggles, sliders
and dropdowns work there too.

The return value is `{ Instance, Columns }`, where `Columns` holds the
containers should you need them later.
