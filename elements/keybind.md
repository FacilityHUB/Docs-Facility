# Keybind

Élément autonome, à distinguer de la pill attachée à un toggle.

```lua
section:Keybind({
    Text = "hold to inspect",
    Flag = "inspect_key",
    Default = "E",
    Mode = "hold",
    Callback = function(down) print(down) end,
})
```

| Option | Défaut | Description |
| --- | --- | --- |
| `Text` | `"keybind"` | libellé |
| `Flag` | `Text` | identifiant de configuration |
| `Default` | `nil` | touche initiale, sous forme de nom (`"E"`, `"MB2"`) |
| `Mode` | `"press"` | `"hold"` appelle `Callback(true)` à l'appui et `Callback(false)` au relâchement |
| `Callback` | `nil` | `function(key)` en mode press, `function(down)` en mode hold |
| `OnChanged` | `nil` | `function(key)` à chaque assignation, effacement compris |

## Interaction

* clic gauche sur la pill : écoute de la prochaine touche ;
* clic gauche ailleurs pendant l'écoute : annulation sans changement ;
* clic droit : efface la touche ;
* `Échap` : efface la touche.

Souris supportée : `MB1`, `MB2`, `MB3`. Pendant une écoute, le raccourci d'ouverture de l'interface est neutralisé pour ne pas se déclencher.

## Méthodes

```lua
keybind:Set("R")
keybind:Get() -- "R", ou "" si aucune touche
```

## Piloter le raccourci du menu

```lua
section:Keybind({
    Text = "menu key",
    Default = "RightShift",
    OnChanged = function(key)
        Library:SetToggleKey(key)
    end,
})
```

C'est exactement ce que fait l'`InterfaceManager`.
