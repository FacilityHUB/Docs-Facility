# Hotkey panel

Lists the keybinds that are currently active, on screen, even with the interface
closed.

```lua
Library:SetHotkeysVisible(true)
```

[Interface manager](interface-manager.md) adds a `hotkeys panel` checkbox that
drives the same thing, so most scripts need no code at all.

## What appears

| Case | Shown as |
| --- | --- |
| toggle with a keybind, toggle on | name and key in the accent colour |
| toggle with a keybind, toggle off | name and key greyed out |
| standalone keybind in `toggle` mode | always listed, accent when active |
| standalone keybind in `press` or `hold` mode | only while the key is held |
| no key assigned | not listed |

The panel hides itself entirely when nothing qualifies, rather than showing an
empty frame.

Every keybind registers itself, so nothing has to be declared.

## Options

```lua
Library:CreateHotkeyPanel({
    Title    = "hotkeys",
    Icon     = "keyboard",
    Width    = 180,
    Position = UDim2.fromOffset(18, 90),
})
```

The panel is draggable. It follows the theme like the rest of the interface.

## Custom entries

Anything can be listed by registering a reader:

```lua
Library:RegisterHotkey(function()
    return {
        Label   = "aimbot",
        Key     = "F",
        Active  = aimbotEnabled,
        Visible = true,
    }
end)
```

The function is polled on every refresh, so the state shown is always current.
Returning `Visible = false` hides that line without removing it.

`Library:RefreshHotkeys()` forces a rebuild, which the library already does on
every toggle, rebind, key press and theme change.
