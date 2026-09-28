# Themes

Twenty three colours drive the whole interface. Change one and everything using
it repaints immediately.

## Palette keys

| Group | Keys |
| --- | --- |
| Accent | `Accent`, `AccentSoft`, `AccentDim` |
| Surfaces | `Window`, `TopBar`, `Section`, `Group`, `Field`, `FieldHover`, `PopupBg`, `Track` |
| Borders | `WindowBorder`, `SectionBorder`, `GroupBorder`, `Border`, `BorderSoft`, `PopupBorder` |
| Text | `Text`, `TextDim`, `TextBright`, `TextMarked`, `TextCode`, `Danger` |

Also on `Library.Theme`: `Font`, `FontMedium`, `TextSize`, `Radius`,
`WindowAlpha`.

## Presets

Eight ship with the library: `facility`, `darker`, `typewriter`, `aqua`,
`amethyst`, `rose`, `contrast`, `light`.

Each declares only a background and an accent; the other twenty one colours are
derived from those in fixed steps. `light` reverses the direction so surfaces
darken instead of lightening, and swaps the text colours.

```lua
ThemeManager:Apply("amethyst")
ThemeManager:SetAccent(Color3.fromRGB(120, 190, 255))
ThemeManager:Names()
```

## Changing a single colour

```lua
Library:SetColor("Section", Color3.fromRGB(29, 29, 32))
Library:SetColor("Section", Color3.fromRGB(29, 29, 32), 0.6)   -- with alpha
```

Alpha maps to the matching transparency property, so a surface can be made
translucent. It only applies to instances that are currently visible, which
keeps an unchecked toggle box from reappearing.

## The editor

```lua
ThemeManager:Mount(Window)
```

Adds a paintbrush to the footer. It opens a modal with the preset dropdown, the
twenty three pickers with readable names, and a reset button.

The backdrop is disabled for this modal, so the interface keeps its real colours
while they are being edited.

Closing with unsaved changes asks whether to save or discard. Discarding
restores the palette captured when the modal opened.

## Saving

```lua
ThemeManager:Save()   -- writes <folder>/settings/theme.json
ThemeManager:Load()   -- last line of the script
```

`Library:Window` reads the same file on its own before drawing anything, which
is what keeps the key system and the interface on one palette.

## How recolouring works

Instances declare which palette key each colour property follows:

```lua
New("Frame", {
    BackgroundColor3 = Theme.Section,
    ThemeTag = { BackgroundColor3 = "Section" },
})
```

`Library:Repaint()` walks that registry and reapplies the palette, dropping
instances whose parent is gone as it goes.

Colours that are computed rather than set once need a hook: the text of a
keybind, the state of a toggle, the active tab.

```lua
Library:OnRepaint(function()
    -- reapply whatever your own element derives from the palette
end)
```

A colour that must not follow the theme should say so:

```lua
New("Frame", {
    BackgroundColor3 = Color3.fromRGB(0, 0, 0),
    ThemeTag = { BackgroundColor3 = false },
})
```

Without that, a black backdrop once matched the `contrast` preset's window
colour by value, inherited its alpha, turned opaque and hid the interface.
