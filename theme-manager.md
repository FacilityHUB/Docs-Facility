# Theme manager

Presets, per colour editing and saving. The colour model itself is described in
[Themes](themes.md).

```lua
ThemeManager:SetLibrary(Library)
ThemeManager:SetFolder("Facility")
ThemeManager:Mount(Window)

-- last line of the script
ThemeManager:Load()
```

## Mount

`Mount(window)` adds a paintbrush icon to the left of the footer, opening the
editor modal.

The modal holds the preset dropdown, the twenty three colour pickers and a reset
button. Closing with unsaved changes asks whether to save or discard.

## API

```lua
ThemeManager:Apply("aqua")
ThemeManager:SetAccent(Color3.fromRGB(120, 190, 255))
ThemeManager:Names()          -- the preset names
ThemeManager:Save()
ThemeManager:Load()
ThemeManager.AutoSave = true  -- write on every change
```

## When to call Load

`ThemeManager:Load()` must be the last line of the script, after every element
exists. Called earlier it repaints an interface that is not built yet.

`Library:Window` separately reads the same file before drawing anything, so the
key system and the window already share the palette. `Load` exists to sync the
editor's pickers with what was loaded.

## Saved file

`<folder>/settings/theme.json`, holding the preset name and the twenty three
colours as `#RRGGBBAA`.

```lua
ThemeManager:SetFolder("Facility")
```
