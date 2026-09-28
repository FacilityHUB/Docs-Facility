# Panels

A panel is a small window of its own, living in a separate `ScreenGui`. It stays
on screen when the main interface is closed, which makes it the right place for
information you want while playing.

```lua
local hud = Library:Panel({
    Title    = "player",
    Icon     = "user",
    Width    = 200,
    Position = UDim2.fromOffset(18, 320),
    Visible  = false,
})

hud.Content:Label("health", { Style = "dim" })
local health = hud.Content:Label("-", { Style = "success" })

hud:SetVisible(true)
```

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Title` | string | – | header text, omit for a bare card |
| `Icon` | string | – | Lucide icon in the header |
| `Width` | number | `180` | width in pixels |
| `Height` | number | – | fixed height, otherwise it follows the content |
| `Position` | UDim2 | `(18, 90)` | starting position |
| `Visible` | boolean | `true` | `false` creates it hidden |
| `Draggable` | boolean | `true` | `false` pins it in place |
| `Collapsed` | boolean | `false` | start folded to the title bar |
| `Name` | string | random | `ScreenGui` name |

## Methods

```lua
hud:SetVisible(true)
hud:Toggle()                              -- collapse or expand
hud:SetOpen(false)
hud:SetPosition(UDim2.fromOffset(40, 40))
hud:Destroy()
hud.Open                                  -- collapsed state
```

## Content

`Content` is a normal container. Every element works: toggles, sliders,
dropdowns, colour pickers, tables, images, `Split`, `Divider`.

```lua
local tools = Library:Panel({ Title = "tools", Width = 240 })

tools.Content:Toggle({
    Text = "auto farm",
    Flag = "hud_farm",
    Callback = function(state) farming = state end,
})

tools.Content:Slider({ Text = "speed", Min = 16, Max = 100, Default = 16 })
```

Dropdowns and colour pickers open in the panel's own popup layer, so they work
with the main interface hidden.

Width matters: 180 is fine for labels, but a toggle carrying a keybind pill and
a gear needs 220 or more.

## Collapsing

With a `Title`, the header shows a chevron on its right. Clicking it folds the
panel to its title bar, which stays draggable. The rest of the header remains a
drag handle, so folding never happens by accident while moving the panel.

## Live values

```lua
local hudVisible = false

task.spawn(function()
    while task.wait(0.5) do
        if hudVisible then
            local character = game.Players.LocalPlayer.Character
            local humanoid = character and character:FindFirstChildOfClass("Humanoid")
            health:Set(humanoid and math.floor(humanoid.Health) or "-")
        end
    end
end)
```

Guard the loop on the panel's visibility. Without it the work keeps happening
while nothing is on screen.

## Gating it behind a toggle

```lua
local panel = Library:Panel({ Title = "player", Visible = false })

section:Toggle({
    Text = "player panel",
    Flag = "player_panel",
    Callback = function(state)
        panelVisible = state
        panel:SetVisible(state)
    end,
})
```

The flag saves the state with the rest of the config, so the panel comes back on
its own next session.

## Several panels

Create as many as needed; each is independent, with its own position and
collapsed state. Give each one a `Position`, otherwise they all stack at the
same default spot.
