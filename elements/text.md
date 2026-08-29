# Textes et paragraphes

## Label

```lua
section:Label("no groups found.")
section:Label("all systems nominal.", { Style = "success", Icon = "check" })
section:Label("valeur brute", Color3.fromRGB(200, 200, 200))
```

| Option | Défaut | Description |
| --- | --- | --- |
| `Style` | `nil` | voir la liste des styles |
| `Color` | `TextDim` | couleur explicite, prioritaire sur `Style` |
| `Icon` | `nil` | nom Lucide, identifiant numérique ou `rbxassetid://` |
| `TextSize` | `13` | taille |
| `Font` | `Gotham` | police |

Le texte est renvoyé à la ligne automatiquement, la hauteur suit le contenu.

```lua
local label = section:Label("chargement…")
label:Set("terminé")
label:SetStyle("success")
label:SetColor(Color3.fromRGB(255, 0, 0))
```

## Paragraph

Carte encadrée avec titre, icône et corps de texte : utile pour les explications et les avertissements.

```lua
section:Paragraph({
    Title = "careful",
    Content = "Changer ce réglage relance la boucle principale.",
    Style = "warning",
    Icon = "alert-triangle",
})
```

| Option | Défaut | Description |
| --- | --- | --- |
| `Title` | `""` | titre, coloré par le style |
| `Content` | `nil` | corps de texte |
| `Style` | `nil` | teinte du titre, de l'icône et du contour |
| `Icon` | `nil` | icône devant le titre |
| `ContentColor` | `TextDim` | couleur du corps |
| `TextSize` | `12` | taille du corps |

```lua
local para = section:Paragraph({ Title = "état", Content = "…" })
para:Set({ Title = "erreur", Content = "fichier introuvable", Style = "danger" })
```

## Styles

| Nom | Couleur |
| --- | --- |
| `normal`, `text` | gris clair |
| `dim`, `muted` | gris |
| `bright`, `title` | blanc cassé |
| `warning`, `warn`, `yellow` | jaune |
| `danger`, `error`, `red` | rouge |
| `success`, `green` | vert |
| `accent`, `pink` | couleur d'accent |

Une `Color3` peut être passée directement à la place d'un nom de style.
