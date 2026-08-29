# Input et Search

## Input

Champ de texte avec légende au-dessus.

```lua
local input = section:Input({
    Text = "name",
    Flag = "config_name",
    Default = "default",
    Placeholder = "config name",
    Callback = function(text, enterPressed) print(text) end,
})

input:Get()
input:Set("valeur")
```

| Option | Défaut | Description |
| --- | --- | --- |
| `Text` | `nil` | légende |
| `Flag` | `Text` | identifiant de configuration |
| `Default` | `""` | texte initial |
| `Placeholder` | `""` | texte grisé |
| `Callback` | `nil` | `function(text, enterPressed)` à la perte de focus |

## Search

Champ suivi d'un libellé à droite, prévu pour filtrer une liste.

```lua
section:Search({
    Label = "search",
    Placeholder = "",
    Live = true,
    Flag = nil,
    Callback = function(text) print(text) end,
})
```

| Option | Défaut | Description |
| --- | --- | --- |
| `Label` | `"search"` | libellé à droite du champ |
| `Placeholder` | `""` | texte grisé |
| `Default` | `""` | texte initial |
| `Live` | `false` | déclenche le callback à chaque frappe au lieu de la perte de focus |
| `Flag` | `nil` | non sauvegardé sauf si fourni explicitement |
| `Callback` | `nil` | `function(text, enterPressed)` |

Contrairement aux autres éléments, `Search` n'utilise pas `Text` comme flag par défaut : sans `Flag`, il reste hors des configurations.
