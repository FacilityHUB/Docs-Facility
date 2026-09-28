# Dialogs

## Confirmations

```lua
Window:Confirm({
    Title     = "unload",
    Text      = "Unload the interface? Unsaved changes will be lost.",
    Confirm   = "unload",
    Cancel    = "cancel",
    OnConfirm = function() Library:Destroy() end,
    OnCancel  = function() end,
    OnDismiss = function() end,
})
```

| Option | Default | Effect |
| --- | --- | --- |
| `Title` | `"confirm"` | header |
| `Text` | `"are you sure?"` | body |
| `Confirm` | `"save"` | right button label |
| `Cancel` | `"discard"` | left button label |
| `OnConfirm` | – | runs on confirm |
| `OnCancel` | – | runs on cancel |
| `OnDismiss` | – | closed with Escape, the cross or the backdrop |

The buttons sit at the bottom of the card, so a longer message pushes the text
rather than the buttons.

The library uses this for unloading, for deleting a config, and when the theme
editor closes with unsaved changes.

## Modals

A modal is a card centred over the window that holds any element.

```lua
local modal = Window:Modal({
    Title  = "settings",
    Width  = 300,
    Height = 0.82,
    Dim    = 0.25,
    Blur   = 16,
})

modal.Content:Toggle({ Text = "an option" })
modal.Content:Slider({ Text = "a value", Min = 0, Max = 10 })

modal:SetOpen(true)
modal:Toggle()
modal.OnClose = function() print("closed") end
```

| Option | Default | Effect |
| --- | --- | --- |
| `Title` | `"panel"` | header |
| `Width` | `340` | width in pixels |
| `Height` | `0.78` | fraction of the window, or pixels above `1` |
| `Dim` | `0.25` | backdrop darkness, `0` removes it |
| `Blur` | `16` | blurs the 3D scene, `0` disables |

It closes on the cross, on the backdrop, or with Escape. `Content` scrolls when
the content is taller than the card.

## About the backdrop

Roblox cannot blur one interface behind another. `Blur` acts on the 3D scene and
`Dim` darkens the interface with a translucent overlay.

Set both to `0` when the user has to see what is behind, which is what the theme
editor does so colours can be judged as they change.
