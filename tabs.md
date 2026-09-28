# Tabs

## Creating a tab

```lua
local Main     = Window:Tab("main")                              -- no icon
local Display  = Window:Tab("display", "monitor")                -- Lucide icon
local Settings = Window:Tab({ Title = "settings", Icon = "cog" })
```

All three forms work. Icons are optional; an unknown name draws nothing instead
of erroring.

```lua
Window:SetTab(Main)   -- select a tab from code
```

The first tab created is selected by default.

## Layouts

```lua
local Window = Library:Window({
    TabStyle = "top",    -- default, tabs in the header
})

local Window = Library:Window({
    TabStyle = "side",   -- tabs in a left column
    TabWidth = 140,
})
```

`CategoryMod = 1` and `CategoryMod = 2` are accepted as aliases.

**Top** keeps the header compact and suits five or six tabs. Beyond that the
bar scrolls horizontally.

**Side** gives each tab a full row with its icon, and the active one gets an
accent bar on its left edge. Better for long lists, and easier to hit on mobile.

The content area shifts automatically, nothing else in your script changes.

## Dividers

```lua
local Main    = Window:Tab("main", "home")
local Combat  = Window:Tab("combat", "swords")

Window:TabDivider()

local Visuals = Window:Tab("visuals", "eye")

Window:TabDivider({ Text = "advanced" })

local Config  = Window:Tab("config", "cog")
```

| Option | Default | Effect |
| --- | --- | --- |
| `Text` | – | draws a small caption instead of a line |
| `Inset` | `12` | horizontal margin |
| `Height` | `11` | vertical space taken |

Dividers only appear in side mode. In top mode the call returns `nil` and does
nothing, so the same script works in both layouts without a condition.
