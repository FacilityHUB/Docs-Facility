# Boutons

## Button

```lua
section:Button({
    Text = "reload scripts",
    Callback = function()
        print("clic")
    end,
})
```

Pleine largeur, 26 px de haut.

## ButtonRow

Deux à trois boutons de largeur égale sur une même ligne.

```lua
section:ButtonRow({
    { Text = "save", Callback = function() end },
    { Text = "load", Callback = function() end },
})
```

Retourne `{ Instance, Buttons }`, `Buttons` contenant les `TextButton` dans l'ordre fourni.

## Action de footer

```lua
Window:Action("Connect", function()
    Library:Notify("demoui", "connected.", 3)
end)
```

Bouton texte en couleur d'accent, aligné à droite dans la barre du bas. Plusieurs appels empilent les actions de droite à gauche.

## Divider

```lua
section:Divider()
```

Ligne de séparation d'un pixel.

Aucun de ces éléments n'a d'état, ils ne sont donc jamais enregistrés dans les configurations.
