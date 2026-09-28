# Mobile

## The floating button

On touch devices a round button appears so the interface can be opened without a
keyboard. It is created automatically.

```lua
local Window = Library:Window({
    MobileButton = true,    -- force it on desktop too
    MobileButton = false,   -- never create it
})
```

```lua
Library:SetMobileButtonVisible(false)

Library:CreateMobileButton({
    Size     = 46,
    Position = UDim2.fromOffset(20, 200),
})
```

Drag it to move it, tap it to toggle the interface. Dragging never triggers the
toggle.

## What to watch for

**Element sizes.** Rows are 22 to 26 px tall, comfortable with a mouse, tight
with a thumb. Prefer fewer options per section on a script aimed at mobile.

**Hover states.** There is no hover on touch, so anything that only reveals
itself on hover is invisible there. The library does not rely on hover for
anything essential, and your own code should not either.

**Panel width.** A [panel](panels.md) at its default 180 px is hard to use on a
phone. Go to 240 or more, or rely on the main interface instead.

**Tab layout.** Side tabs give each entry a full row, which is easier to hit than
a horizontal bar. Worth switching to `TabStyle = "side"` for a mobile audience.

## Multi touch

Dragging the window, a panel or a dialog only follows the finger that started
the drag. Rotating the camera with another finger at the same time no longer
moves the interface.
