# Toggle

Case à cocher : carré vide au repos, rempli en couleur d'accent une fois actif. Le label ne change pas de couleur.

```lua
local toggle = section:Toggle({
    Text = "enable",
    Flag = "enable",
    Default = false,
    Hint = "active la boucle principale",
    Callback = function(state)
        print(state)
    end,
})
```

| Option | Défaut | Description |
| --- | --- | --- |
| `Text` | `"toggle"` | libellé |
| `Flag` | `Text` | identifiant de configuration, `false` pour exclure |
| `Default` | `false` | état initial ; si `true`, le `Callback` est appelé à la construction |
| `Hint` | `nil` | ajoute un `?` avec infobulle au survol |
| `Callback` | `nil` | `function(state)` |

## Méthodes

```lua
toggle:Set(true)        -- déclenche le callback
toggle:Set(true, true)  -- silencieux
toggle.State            -- booléen courant
```

## Éléments attachés

Les trois méthodes suivantes retournent le toggle, donc elles se chaînent.

### Keybind

Pill à droite de la ligne. Clic gauche pour écouter, clic gauche ailleurs pour annuler, clic droit pour effacer.

```lua
toggle:Keybind({ Default = "F", Flag = "enable_key", Mode = "hold" })
```

`Mode = "hold"` active le toggle tant que la touche est maintenue. Sans `Flag`, la touche n'est pas sauvegardée.

### Color picker

Une ou plusieurs pastilles à droite, chacune avec son propre flag et son propre callback.

```lua
toggle
    :ColorPicker({ Flag = "outline", Default = Color3.fromRGB(232, 161, 168) })
    :ColorPicker({ Flag = "fill", Default = Color3.fromRGB(60, 60, 65), DefaultAlpha = 0.35 })

toggle.Pickers[1]:Get() -- Color3, alpha
```

### Gear

Icône d'engrenage ouvrant un panneau flottant qui accepte tous les éléments.

```lua
toggle:Gear(function(panel)
    panel:Slider({ Text = "delay", Flag = "delay", Min = 0, Max = 500, Suffix = " ms", Default = 60 })
    panel:Dropdown({ Text = "profile", Flag = "profile", Options = { "default", "custom" } })
end)
```

## Ordre d'affichage

Pastilles de couleur, puis pill keybind, puis engrenage. La largeur du label se recalcule automatiquement pour ne jamais être tronquée.
