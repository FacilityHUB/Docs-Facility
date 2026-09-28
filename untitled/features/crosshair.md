# Crosshair

Some games hide the mouse pointer, which makes an interface hard to use. The
crosshair draws one while the interface is open and disappears with it.

```lua
local Window = Library:Window({
    Cursor = true,
})
```

## Options

```lua
Cursor = {
    Length    = 9,                          -- length of one arm
    Thickness = 2,
    Gap       = 4,                          -- empty space at the centre
    Dot       = true,                       -- centre dot
    Color     = Color3.fromRGB(0, 255, 0),  -- defaults to the accent colour
},
```

Four arms around an optional dot, with a gap in the middle. Drawn in the accent
colour by default, so it follows the theme.

## From code

```lua
Library:SetCursor(true)
Library:SetCursor(false)
Library.CursorEnabled
```

Useful behind a toggle:

```lua
section:Toggle({
    Text = "crosshair",
    Flag = "crosshair",
    Callback = function(state) Library:SetCursor(state) end,
})
```

Do not set `Cursor = true` on the window in that case, or it will be on before
the toggle is ever touched.

## Behaviour

It follows the mouse on the last render step, so it matches the pointer with no
visible lag. It lives in its own `ScreenGui` above everything else, and only
draws while the interface is open.
