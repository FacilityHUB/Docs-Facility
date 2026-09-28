# Facility

Facility is a UI library for Roblox executors. It gives a script a complete
interface: tabs, sections, sixteen element types, a live theme editor, floating
panels, config saving, a key system and a server browser.

```lua
local BASE = "https://raw.githubusercontent.com/FacilityHUB/UI-Facility/refs/heads/main/"

local Library = loadstring(game:HttpGet(BASE .. "main.luau"))()
Library.BaseUrl = BASE

local Window = Library:Window({
    Title  = "facility",
    Suffix = ".app",
})

local Main = Window:Tab("main", "home")
local section = Main:Section("global", 1)

section:Toggle({
    Text = "auto farm",
    Flag = "auto_farm",
    Callback = function(state)
        print("auto farm:", state)
    end,
})
```

## What it covers

Two tab layouts, top bar or left column. Two card title styles. Sixteen
elements, each one able to save its value to a config file. A theme system with
eight presets and twenty three individually editable colours that recolour the
interface live. Floating panels that stay on screen when the interface is
closed. A key system that blocks the script until a valid key is entered.

## Requirements

An executor with `game:HttpGet`. File functions (`writefile`, `readfile`,
`isfile`, `listfiles`) are needed for config and theme saving; without them the
library still runs and saving is simply unavailable.

Start with [Getting started](getting-started.md).
