# Interface manager

Settings that belong to the user rather than to the script.

```lua
InterfaceManager:SetLibrary(Library)
InterfaceManager:SetWindow(Window)
InterfaceManager:SetFolder("Facility")
InterfaceManager:BuildInterfaceSection(Settings, 1)
```

## The built section

**menu key** rebinds the key that shows and hides the interface.

**ui scale** resizes everything between 70 and 130 percent, for high resolution
screens or small ones.

**hotkeys panel** shows the on screen list of active keybinds, see
[Hotkey panel](hotkey-panel.md).

**unload** destroys the interface, behind a confirmation.

## Flags

`interface_menu_key`, `interface_scale`, `interface_hotkeys`.

They are excluded from configs by `SaveManager:IgnoreThemeSettings()`, and live
for the session only: they are not written to disk.

## Order

`SetWindow` must be called before `BuildInterfaceSection`, since the section
needs the window to act on it.
