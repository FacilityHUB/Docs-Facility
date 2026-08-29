# Color picker

Ligne avec pastille à droite ; le clic ouvre un panneau flottant : carré saturation/valeur, barre de teinte, barre d'alpha, champ hexadécimal et liens `copy` / `paste`.

```lua
local picker = section:ColorPicker({
    Text = "highlight",
    Flag = "highlight_color",
    Default = Color3.fromRGB(232, 161, 168),
    DefaultAlpha = 1,
    Callback = function(color, alpha)
        print(color, alpha)
    end,
})
```

| Option | Défaut | Description |
| --- | --- | --- |
| `Text` | `"color"` | libellé (ignoré pour une pastille attachée à un toggle) |
| `Flag` | `Text` | identifiant de configuration |
| `Default` | blanc | `Color3` initial |
| `DefaultAlpha` | `1` | alpha initial, de `0` à `1` |
| `Alpha` | `true` | `false` retire la barre d'alpha |
| `Callback` | `nil` | `function(color, alpha)` |

## Méthodes

```lua
picker:Get()                                  -- Color3, alpha
picker:Set(Color3.fromRGB(255, 0, 0))
picker:Set("#FF0000AA")                       -- hex, alpha inclus
picker:Set(Color3.new(1, 0, 0), 0.5, true)    -- silencieux
picker.Color
picker.Alpha
```

## Format de sauvegarde

La valeur stockée est une chaîne `#RRGGBBAA`. `Set` accepte indifféremment une `Color3` ou une chaîne hexadécimale de 6 ou 8 caractères, avec ou sans `#`.

## Plusieurs pickers sur une même option

```lua
section:Toggle({ Text = "radius circle", Flag = "radius" })
    :ColorPicker({ Flag = "radius_outline", Default = Color3.fromRGB(232, 161, 168) })
    :ColorPicker({ Flag = "radius_fill", Default = Color3.fromRGB(60, 60, 65), DefaultAlpha = 0.35 })
```

L'alpha est rendu visible sur la pastille, ce qui distingue au premier coup d'œil un contour opaque d'un remplissage translucide.
