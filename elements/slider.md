# Slider

```lua
local slider = section:Slider({
    Text = "radius",
    Flag = "radius",
    Min = 0,
    Max = 200,
    Default = 50,
    Suffix = " m",
    Callback = function(value) print(value) end,
})
```

| Option | Défaut | Description |
| --- | --- | --- |
| `Text` | `"slider"` | libellé |
| `Flag` | `Text` | identifiant de configuration |
| `Min` / `Max` | `0` / `100` | bornes |
| `Default` | `Min` | valeur initiale |
| `Step` | `nil` | incrément d'arrondi |
| `Decimals` | `0` | décimales affichées et conservées |
| `Suffix` | `nil` | texte collé après la valeur |
| `ZeroText` | `nil` | texte de remplacement quand la valeur vaut `Min` |
| `Callback` | `nil` | `function(value)` |

## Exemples

```lua
section:Slider({ Text = "strength", Flag = "strength", Min = 0, Max = 1, Decimals = 2, Default = 0.35 })
section:Slider({ Text = "max distance", Flag = "distance", Min = 0, Max = 5000, Default = 0, ZeroText = "0 - unlimited" })
section:Slider({ Text = "steps", Flag = "steps", Min = 0, Max = 100, Step = 5, Default = 25 })
```

## Méthodes

```lua
slider:Set(120)
slider:Set(120, true) -- silencieux
slider.Value
```

La zone cliquable dépasse le rail de quelques pixels en hauteur, pour rester utilisable à la souris comme au doigt.
