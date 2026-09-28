# Getting started

## Loading the library

```lua
local BASE = "https://raw.githubusercontent.com/FacilityHUB/UI-Facility/refs/heads/main/"

local Library = loadstring(game:HttpGet(BASE .. "main.luau"))()
Library.BaseUrl = BASE
```

`Library.BaseUrl` must be set before anything else. The library fetches its
addons from that URL, and without it `Library.SaveManager` and the others stay
`nil`.

## A complete script

```lua
local BASE = "https://raw.githubusercontent.com/FacilityHUB/UI-Facility/refs/heads/main/"

local Library = loadstring(game:HttpGet(BASE .. "main.luau"))()
Library.BaseUrl = BASE

local SaveManager      = Library.SaveManager
local InterfaceManager = Library.InterfaceManager
local ThemeManager     = Library.ThemeManager

-- 1. window
local Window = Library:Window({
    Title  = "facility",
    Suffix = ".app",
    Width  = 640,
    Height = 560,
})

-- 2. tabs
local Main     = Window:Tab("main", "home")
local Settings = Window:Tab("settings", "cog")

-- 3. sections and elements
local combat = Main:Section("combat", 1)

combat:Toggle({
    Text = "aimbot",
    Flag = "aimbot",
    Callback = function(state) print(state) end,
}):Keybind({ Default = "E", Flag = "aimbot_key" })

combat:Slider({
    Text = "fov",
    Flag = "aimbot_fov",
    Min = 10, Max = 400, Default = 120,
})

-- 4. managers, always last
SaveManager:SetLibrary(Library)
InterfaceManager:SetLibrary(Library)
InterfaceManager:SetWindow(Window)
ThemeManager:SetLibrary(Library)

SaveManager:IgnoreThemeSettings()
InterfaceManager:SetFolder("Facility")
ThemeManager:SetFolder("Facility")
SaveManager:SetFolder("Facility/game")

InterfaceManager:BuildInterfaceSection(Settings, 1)
SaveManager:BuildConfigSection(Settings, 2)
ThemeManager:Mount(Window)

Window:SetTab(Main)

Library:Notify("facility", "loaded.", 4)

SaveManager:LoadAutoloadConfig()
ThemeManager:Load()
```

## Order matters

Managers come last, once every element exists. `SaveManager` captures the
default value of each flag when its section is built, and `ThemeManager:Load()`
has to repaint instances that already exist.

`ThemeManager:Load()` is the last line of the script. Called earlier it repaints
an interface that is not built yet and does nothing.

## Checking what is loaded

```lua
print(Library.Version)
```

Raw file hosts cache aggressively. If a change does not show up, that print will
tell you whether the build you expect is really running. While testing you can
force a fresh copy:

```lua
local source = game:HttpGet(BASE .. "main.luau?v=" .. tostring(tick()))
```

Remove it once done, it defeats caching entirely and costs a full download per
run.
