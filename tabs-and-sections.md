# Onglets et sections

## Onglets

```lua
local General = Window:Tab("general")
local Settings = Window:Tab("settings")

Window:SetTab(General)
Window:SetTab("settings") -- par nom
```

La barre d'onglets défile horizontalement quand les onglets dépassent la largeur disponible : rien ne sort de la fenêtre, même après un redimensionnement.

## Colonnes

Chaque onglet a deux colonnes de largeur égale. Le second argument de `Section` choisit la colonne (`1` par défaut).

```lua
local left  = General:Section("global", 1)
local right = General:Section("settings", 2)
```

Équivalent explicite :

```lua
local column = General:Column(2)
local section = column:Section("settings")
```

## Sections

Une section est une carte au titre cliquable : le clic replie ou déplie son contenu avec animation.

```lua
local section = General:Section("global", 1)

section.Open      -- état courant
section.Frame     -- l'instance
section.Container -- le conteneur des éléments
```

Toutes les méthodes d'éléments s'appellent sur une section :

```lua
section:Toggle({ ... })
section:Dropdown({ ... })
section:Slider({ ... })
section:Keybind({ ... })
section:ColorPicker({ ... })
section:Input({ ... })
section:Search({ ... })
section:Button({ ... })
section:ButtonRow({ ... })
section:Label("texte")
section:Paragraph({ ... })
section:Divider()
```

Les popups d'engrenage exposent exactement les mêmes méthodes, ce qui permet d'imbriquer n'importe quel élément.
