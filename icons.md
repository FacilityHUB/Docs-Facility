# Icônes

Les icônes utilisent la bibliothèque Lucide, chargée depuis le dépôt de Rayfield.

```lua
Library.IconSource = "https://raw.githubusercontent.com/SiriusSoftwareLtd/Rayfield/refs/heads/main/icons.lua"
```

Le chargement est différé au premier usage puis mis en cache. Pour le forcer :

```lua
Library:PreloadIcons()
```

## Formats acceptés

```lua
Icon = "alert-triangle"        -- nom Lucide
Icon = 4483362458              -- identifiant d'asset
Icon = "rbxassetid://4483362458"
```

Un nom introuvable ou une bibliothèque indisponible n'entraîne pas d'erreur : l'élément s'affiche simplement sans icône.

## Où les utiliser

`Label`, `Paragraph` et les notifications. La couleur de l'icône suit le style de l'élément.

## Trouver un nom

Les noms varient selon la version du fichier `icons.lua` — par exemple `alert-triangle` contre `triangle-alert`. Pour lister ce qui est réellement disponible :

```lua
for name in pairs(Library:PreloadIcons()["48px"]) do
    print(name)
end
```
