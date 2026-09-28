# Window

The window is the frame that holds everything: header, tabs, content and footer.

```lua
local Window = Library:Window({
    Title  = "facility",
    Suffix = ".app",
})
```

## Options

| Option              | Type          | Default      | Effect                                      |
| ------------------- | ------------- | ------------ | ------------------------------------------- |
| `Title`             | string        | `"facility"` | left part of the header                     |
| `Suffix`            | string        | `".app"`     | appended in the accent colour               |
| `Width`             | number        | `620`        | starting width                              |
| `Height`            | number        | `560`        | starting height                             |
| `MinWidth`          | number        | `420`        | resize floor                                |
| `MinHeight`         | number        | `300`        | resize floor                                |
| `TabStyle`          | string        | `"top"`      | `"top"` or `"side"`                         |
| `TabWidth`          | number        | `140`        | column width in side mode                   |
| `SectionTitleStyle` | string        | `"inline"`   | `"inline"` or `"border"`                    |
| `Footer`            | boolean       | `true`       | `false` removes the footer                  |
| `MobileButton`      | boolean       | auto         | force the floating button                   |
| `Cursor`            | boolean/table | `false`      | crosshair while open                        |
| `ThemeFolder`       | string        | `"Facility"` | folder the saved theme is read from         |
| `KeySystem`         | boolean       | `false`      | see [Key system](../features/key-system.md) |
| `KeySettings`       | table         | –            | key system configuration                    |
| `Discord`           | table         | –            | Discord invite through the local RPC        |

## Size and scale

```lua
Window:SetSize(720, 600)
Window:SetUserScale(1.2)   -- 0.6 to 1.4, scales the whole interface
Window:SetOpacity(0.9)     -- 0.2 to 1
```

The window is draggable by its header and resizable from the bottom right corner. Both respect `MinWidth` and `MinHeight`.

## Visibility

```lua
Library:SetToggleKey("RightShift")   -- key name, "MB2", or an Enum.KeyCode
Library:ToggleUI()                   -- flips
Library:ToggleUI(true)               -- forces
Library.Open                         -- current state

Window:SetVisible(false)             -- this window only
```

The toggle key is also configurable by the user through [Interface manager](../configuration/interface-manager.md).

## Footer

```lua
Window:Action("Connect", function()
    Library:Notify("facility", "connected.", 3)
end)

Window:IconAction("paintbrush", function()
    print("icon clicked")
end)
```

`Action` adds a text button on the right, `IconAction` an icon on the left. [Theme manager](../configuration/theme-manager.md) uses `IconAction` for its paintbrush.

## Discord

Sends an invite request to the Discord client running on the machine. There is no UI: the player gets Discord's own native prompt. Nothing happens when Discord is closed or the executor has no `request` function.

```lua
local Window = Library:Window({
    Discord = {
        Invite        = "xxxxxxx",   -- the code only, without discord.gg/
        RememberJoins = true,        -- skip the request on later runs
    },
})
```

With `RememberJoins`, a marker file is written so the player is not asked again.

## Unloading

```lua
Library:Destroy()
```

Disconnects every tracked connection, destroys every `ScreenGui` including panels, the hotkey panel, the crosshair and the server browser, then clears the registries. [Interface manager](../configuration/interface-manager.md) exposes it as an `unload` button with a confirmation.
