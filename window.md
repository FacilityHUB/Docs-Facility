# Fenêtre

```lua
local Window = Library:Window({
    Title  = "demoui",
    Suffix = ".app",
    Width  = 620,
    Height = 620,
})
```

## Options

| Option | Défaut | Description |
| --- | --- | --- |
| `Title` | `"demoui"` | texte clair de la barre supérieure |
| `Suffix` | `".app"` | suite du titre, affichée en gris |
| `Width` / `Height` | `620` / `560` | taille de départ en pixels |
| `MinWidth` / `MinHeight` | `460` / `320` | bornes basses du redimensionnement |
| `Position` | centré | `UDim2`, ancrage au centre de la fenêtre |
| `Footer` | `true` | `false` retire la barre du bas |
| `Name` | `"DemoUI"` | nom du `ScreenGui` |
| `MobileButton` | auto | `true` force le bouton flottant, `false` le désactive ; par défaut créé si l'appareil est tactile |
| `MobileButtonOptions` | `nil` | `{ Size = 44, Position = UDim2… }` |

## Comportement

**Déplacement** : glisser la barre supérieure.

**Redimensionnement** : poignée en bas à droite. La taille est bornée par `MinWidth`/`MinHeight` et par le viewport. Tout suit automatiquement — colonnes, sections, footer.

**Mise à l'échelle responsive** : un `UIScale` réduit la fenêtre jusqu'à `0.55` si l'écran est trop petit, sans jamais dépasser `1` (multiplié par l'échelle utilisateur).

## Méthodes

```lua
Window:Tab(name)                 -- crée un onglet
Window:SetTab(tabOrName)         -- change d'onglet
Window:Action(text, callback)    -- bouton texte dans le footer
Window:SetVisible(bool)
Window:SetSize(width, height)
Window:SetUserScale(1.15)        -- 0.6 à 1.4
Window:SetOpacity(0.9)           -- 0.2 à 1
Window:CloseFloating()           -- ferme dropdowns et popups ouverts
```

## Champs

`Window.Tabs`, `Window.ActiveTab`, `Window.Main`, `Window.Gui`, `Window.Width`, `Window.Height`, `Window.Visible`.

## Bouton mobile

Bouton flottant dans son propre `ScreenGui`, donc toujours visible même interface masquée. Déplaçable au doigt ; un appui sans déplacement (moins de 6 px) bascule l'interface.

```lua
Library:CreateMobileButton({ Position = UDim2.new(1, -70, 0, 90) })
Library:SetMobileButtonVisible(false)
```
