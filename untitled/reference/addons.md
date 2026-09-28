# Addons

The three managers are addons. Your own follow the same shape.

## Writing one

An addon is a file returning a function that takes the library and returns a
table.

```lua
-- addons/MyAddon.luau
return function(Library)
    local MyAddon = {}

    MyAddon.Library = Library

    function MyAddon:Build(tab, column)
        local section = tab:Section("my feature", column or 1)

        section:Button({
            Text = "run",
            Callback = function()
                self.Library:Notify("my addon", "done.", 3)
            end,
        })
    end

    return MyAddon
end
```

## Loading

```lua
Library.AddonPaths.MyAddon = "addons/MyAddon.luau"
local MyAddon = Library:LoadAddon("MyAddon")

MyAddon:Build(Settings, 1)
```

`LoadAddon` fetches `Library.BaseUrl .. path` and runs it. A missing file gives
a console warning and returns `nil`, so guard the result if the addon is
optional.

## What is available

`Library.Theme` for the palette.

`Library.FileSystem` with `Read`, `Write`, `Delete`, `List`.

`Library:BuildFolders(folder)` to create a folder tree.

`Library:Repaint()` after touching the palette.

`Library:Notify`, `Library:Warn`, `Library:Error`, `Library:Success`.

Every tab, section and element method.

## Conventions worth following

Take the library through `SetLibrary` rather than capturing the upvalue, so an
addon can be pointed at another instance.

Prefix your flags to avoid collisions with the host script.

Expose a `Flags` table listing the ones you own, so the host can exclude them
from configs the way `IgnoreThemeSettings` does.
