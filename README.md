# DemoUI

Librairie d'interface Luau pour Roblox : fenêtre redimensionnable, onglets, sections repliables, éléments modernes, système de configurations et notifications.

## Chargement

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/FacilityHUB/test/refs/heads/main/test15"))()
```

En Studio ou avec Rojo, `DemoUI` est un `ModuleScript` :

```lua
local Library = require(script.Parent:WaitForChild("DemoUI"))
```

## Exemple minimal

```lua
local Window = Library:Window({ Title = "demoui", Suffix = ".app" })

local General = Window:Tab("general")
local section = General:Section("global", 1)

section:Toggle({
    Text = "enable",
    Flag = "enable",
    Callback = function(state)
        print("enable", state)
    end,
})

section:Slider({ Text = "radius", Flag = "radius", Min = 0, Max = 200, Default = 50 })

Window:Action("Connect", function()
    Library:Notify("demoui", "session started.", 3)
end)
```

## Ce que couvre la librairie

| Domaine | Contenu |
| --- | --- |
| Fenêtre | déplacement, redimensionnement, mise à l'échelle responsive, raccourci clavier, bouton mobile |
| Structure | onglets scrollables, deux colonnes, sections repliables |
| Éléments | toggle, dropdown, slider, keybind, color picker, input, search, boutons, labels, paragraphes |
| Données | registre de flags, sauvegarde et chargement de configurations, autoload |
| Retours | notifications avec styles et icônes Lucide |

## Compatibilité

Roblox uniquement, en client. Les fonctions de fichiers (`writefile`, `readfile`, `listfiles`, `delfile`) sont détectées à l'exécution : sans elles, les configurations restent en mémoire pour la session. `setclipboard` et `getclipboard` sont optionnels (boutons copy/paste).
