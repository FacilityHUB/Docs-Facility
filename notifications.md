# Notifications

Cartes empilées en bas à droite, dans leur propre `ScreenGui` : elles restent visibles interface masquée.

## Appels

```lua
Library:Notify("Facility", "script loaded.", 5)

Library:Notify({
    Title = "Facility",
    Text = "script loaded.",
    Duration = 5,
})

Library:Notify({ Title = "Facility", Content = "alias Fluent" })
```

`Text`, `Content` et `Description` sont interchangeables.

| Option | Défaut | Description |
| --- | --- | --- |
| `Title` | `"notice"` | titre |
| `Text` | `nil` | corps, renvoyé à la ligne |
| `Duration` | `3.5` | durée d'affichage en secondes |
| `Style` | `nil` | `warning`, `danger`, `success`, `accent`… |
| `Color` | `nil` | teinte explicite, prioritaire sur `Style` |
| `Icon` | auto | icône devant le titre |

## Raccourcis

```lua
Library:Warn("attention", "option expérimentale.", 4)
Library:Error("risky", "action irréversible.", 4)
Library:Success("done", "config appliquée.", 4)
```

Le style pilote la barre d'accent à gauche, la couleur du titre et l'icône par défaut (`alert-triangle`, `x-circle`, `check-circle`). Sans style : barre rose, titre clair, pas d'icône.

## Couper les notifications

```lua
Library.NotificationsEnabled = false
```

`Library:Notify` retourne immédiatement sans rien afficher.
