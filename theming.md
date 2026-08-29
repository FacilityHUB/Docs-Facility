# Thème

Toutes les couleurs vivent dans `Library.Theme`, lues au moment de la construction des instances.

```lua
Library.Theme.Accent = Color3.fromRGB(120, 190, 255)
```

Cette modification doit intervenir **avant** `Library:Window(...)` : changer le thème après coup ne recolore pas les instances déjà créées.

## Clés

| Clé | Rôle |
| --- | --- |
| `Window`, `WindowAlpha`, `WindowBorder` | fenêtre et son contour |
| `TopBar` | barre supérieure |
| `Section`, `SectionBorder` | cartes de section, notifications |
| `Group`, `GroupBorder` | paragraphes |
| `Field`, `FieldHover`, `Border` | dropdowns, boutons, champs, pills |
| `PopupBg`, `PopupBorder` | panneaux flottants |
| `BorderSoft` | séparateurs |
| `Track` | rail de slider |
| `Text`, `TextDim`, `TextBright` | trois niveaux de texte |
| `TextMarked` | jaune des styles `warning` |
| `TextCode` | vert des styles `success` |
| `Danger` | rouge des styles `danger` |
| `Accent`, `AccentSoft`, `AccentDim` | couleur d'accent, survol, scrollbars |
| `Font`, `FontMedium`, `TextSize`, `Radius` | typographie et arrondi |
| `GearIcon` | asset de l'icône d'engrenage |

## Exemple

```lua
local Theme = Library.Theme
Theme.Accent     = Color3.fromRGB(120, 190, 255)
Theme.AccentSoft = Color3.fromRGB(160, 210, 255)
Theme.AccentDim  = Color3.fromRGB(70, 110, 150)

local Window = Library:Window({ Title = "facility" })
```
