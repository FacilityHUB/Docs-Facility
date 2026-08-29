# Démarrage

## Structure d'un script

L'ordre compte : les managers doivent être construits **après** tous les autres éléments, car `BuildConfigSection` capture les valeurs par défaut au moment de son appel.

```lua
local Library = loadstring(game:HttpGet("URL_DE_DEMOUI"))()

local SaveManager = Library.SaveManager
local InterfaceManager = Library.InterfaceManager

-- 1. fenêtre
local Window = Library:Window({ Title = "facility", Suffix = ".app" })

-- 2. onglets
local Main = Window:Tab("main")
local Settings = Window:Tab("settings")

-- 3. sections et éléments
local combat = Main:Section("combat", 1)
combat:Toggle({ Text = "enable", Flag = "combat_enable" })

-- 4. managers
SaveManager:SetLibrary(Library)
InterfaceManager:SetLibrary(Library)
InterfaceManager:SetWindow(Window)

SaveManager:IgnoreThemeSettings()
SaveManager:SetIgnoreIndexes({})

InterfaceManager:SetFolder("Facility")
SaveManager:SetFolder("Facility/mon-jeu")

InterfaceManager:BuildInterfaceSection(Settings, 1)
SaveManager:BuildConfigSection(Settings, 2)

-- 5. état initial
Window:SetTab(Main)
Library:Notify("Facility", "script loaded.", 5)
SaveManager:LoadAutoloadConfig()
```

## Flags

Chaque élément à état accepte un `Flag`, identifiant unique utilisé pour la sauvegarde et pour `Library.Flags`.

```lua
combat:Slider({ Text = "range", Flag = "combat_range", Min = 0, Max = 100, Default = 25 })

print(Library.Flags.combat_range) --> 25
```

Règles :

* sans `Flag`, la valeur de `Text` est utilisée — deux éléments nommés pareil entrent en collision, un `warn` est émis ;
* `Flag = false` exclut totalement l'élément des configurations ;
* les éléments sans état (`Label`, `Paragraph`, `Button`, `Divider`) n'ont pas de flag.

## Raccourci d'ouverture

`RightShift` par défaut.

```lua
Library:SetToggleKey("RightAlt")      -- nom de touche
Library:SetToggleKey(Enum.KeyCode.F4) -- ou un KeyCode
Library:SetToggleKey("MB2")           -- ou un bouton souris
Library:ToggleUI()                    -- bascule manuelle
```

## Déchargement

```lua
Library:Destroy()
```

Déconnecte toutes les connexions suivies, détruit les `ScreenGui` (fenêtre, notifications, bouton mobile) et vide `Flags` et `Registry`.
