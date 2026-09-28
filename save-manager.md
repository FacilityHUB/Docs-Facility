# Save manager

Writes every flagged element to a JSON file so a user can keep several setups.

```lua
SaveManager:SetLibrary(Library)
SaveManager:SetFolder("Facility/game")
SaveManager:IgnoreThemeSettings()
SaveManager:BuildConfigSection(Settings, 2)
SaveManager:LoadAutoloadConfig()
```

## The built section

`BuildConfigSection(tab, column)` draws a complete interface: a name field, the
list of saved configs, and buttons for save, load, delete, refresh, autoload,
clear autoload, copy, paste and reset.

Deleting asks for confirmation. Everything else is immediate.

The section also shows which config is set to autoload and whether there are
unsaved changes.

## From code

```lua
SaveManager:Save("default")
SaveManager:Load("default.json")
SaveManager:Delete("default.json")
SaveManager:List()

SaveManager:SetAutoload("default.json")
SaveManager:GetAutoload()
SaveManager:ClearAutoload()
SaveManager:LoadAutoloadConfig()
```

`Save` and `Load` return `success, message`, so failures can be reported.

## Autoload

Nothing is restored unless a config is marked for autoload. That is deliberate:
a config can flip twenty options at once, and doing that silently at launch
surprises people.

```lua
SaveManager:LoadAutoloadConfig()   -- honours the marked config, if any
```

To always load a specific one regardless:

```lua
SaveManager:Load("default.json")
```

## Excluding flags

```lua
SaveManager:IgnoreThemeSettings()             -- interface_ and theme_ prefixes
SaveManager:SetIgnoreIndexes({ "temp_flag" })
```

Interface settings are excluded by default. The menu key and the scale belong to
the user, not to a config shared between setups.

## Where files go

```lua
SaveManager:SetFolder("Facility/game")
```

Configs land in `Facility/game/settings/`. Using a per game folder keeps setups
from colliding between scripts.

Requires `writefile`, `readfile`, `isfile` and `listfiles`. Without them the
section still draws and reports the missing support rather than erroring.
