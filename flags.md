# Flags

A flag is the name under which an element stores its value. It is what makes
config saving possible.

```lua
section:Toggle({ Text = "auto farm", Flag = "auto_farm" })
```

## Reading and writing

```lua
Library.Flags["auto_farm"]        -- current value
Library:GetConfig()               -- every flag as a table
Library:LoadConfig(data)
Library:ResetDefaults()           -- back to the values captured at build time
```

Reading `Library.Flags` is the usual way for a script to know a setting without
keeping its own copy:

```lua
task.spawn(function()
    while task.wait() do
        if Library.Flags["auto_farm"] then
            farm()
        end
    end
end)
```

## Which elements have one

Toggle, slider, dropdown, keybind, colour picker, input and search. Buttons,
labels, paragraphs, images, tables and dividers hold no state and take no flag.

An element without a flag works normally, it is simply not saved.

## Naming

Two elements sharing a flag is a mistake: the library warns in the console and
keeps the second one. Prefix by feature to avoid it:

```lua
Flag = "aimbot_enabled"
Flag = "aimbot_fov"
Flag = "aimbot_key"
Flag = "esp_enabled"
```

## Excluding flags from configs

```lua
SaveManager:IgnoreThemeSettings()          -- interface_ and theme_ flags
SaveManager:SetIgnoreIndexes({ "my_flag" })
```

Interface settings are excluded by default, since the menu key and the scale
belong to the user rather than to a config.
