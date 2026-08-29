# Dropdown

```lua
local dropdown = section:Dropdown({
    Text = "anchor",
    Flag = "anchor",
    Options = { "head", "torso", "origin" },
    Default = "head",
    Callback = function(value) print(value) end,
})
```

| Option | Défaut | Description |
| --- | --- | --- |
| `Text` | `nil` | légende au-dessus du champ |
| `Flag` | `Text` | identifiant de configuration |
| `Options` | `{}` | liste des valeurs |
| `Default` | première option | valeur initiale, table si `Multi` |
| `Multi` | `false` | sélection multiple |
| `Empty` | `"none"` | texte quand rien n'est sélectionné |
| `Search` | auto | champ de recherche ; affiché seul au-delà de 8 options, `true` force, `false` retire |
| `MaxHeight` | `154` | hauteur maximale de la liste, en pixels |
| `Callback` | `nil` | `function(value)` — chaîne, ou table si `Multi` |

## Sélection multiple

```lua
section:Dropdown({
    Text = "ignore",
    Flag = "ignore",
    Options = { "friends", "hidden", "inactive" },
    Multi = true,
    Default = { "friends" },
})
```

Le champ affiche les valeurs séparées par des virgules ; la liste reste ouverte entre deux choix.

## Méthodes

```lua
dropdown:Get()
dropdown:Set("torso")
dropdown:Set("torso", true)   -- silencieux
dropdown:SetOptions({ "a", "b", "c" })
```

`SetOptions` reconstruit la liste ; si la valeur courante disparaît, la première option est sélectionnée.

## Recherche

Le champ filtre sur sous-chaîne, insensible à la casse, et la hauteur de la liste s'ajuste au nombre de résultats. Il est vidé à chaque ouverture.
