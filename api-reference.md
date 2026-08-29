# Référence API

## Library

| Méthode | Description |
| --- | --- |
| `Library:Window(opts)` | crée une fenêtre |
| `Library:Notify(opts \| title, text, duration)` | notification |
| `Library:Warn / :Error / :Success(title, text, duration)` | notifications typées |
| `Library:SetToggleKey(key)` | raccourci d'ouverture, nom de touche, `KeyCode` ou `MB1`–`MB3` |
| `Library:ToggleUI(state)` | bascule ou force la visibilité |
| `Library:CreateMobileButton(opts)` | bouton flottant tactile |
| `Library:SetMobileButtonVisible(bool)` | affiche ou masque ce bouton |
| `Library:PreloadIcons()` | charge la bibliothèque d'icônes |
| `Library:GetConfig(ignore)` | table `flag = valeur` |
| `Library:LoadConfig(data, ignore)` | applique une table de valeurs |
| `Library:CaptureDefaults()` | instantané des valeurs courantes |
| `Library:ResetDefaults(ignore)` | restaure cet instantané |
| `Library:Register(flag, entry)` | enregistrement manuel |
| `Library:MarkDirty(flag)` / `:ClearDirty()` | indicateur de modifications |
| `Library:Destroy()` | déchargement complet |

### Champs

| Champ | Contenu |
| --- | --- |
| `Library.Flags` | valeurs brutes indexées par flag |
| `Library.Registry` | `{ Type, Get, Set }` par flag |
| `Library.Defaults` | instantané des valeurs par défaut |
| `Library.Theme` | palette |
| `Library.ToggleKey` / `ToggleInput` | raccourci courant |
| `Library.NotificationsEnabled` | active ou coupe les notifications |
| `Library.Open` | interface visible |
| `Library.Windows` | fenêtres créées |
| `Library.IconSource` | URL de `icons.lua` |
| `Library.SaveManager` / `InterfaceManager` | managers |

## Types du registre

| Type | Valeur stockée |
| --- | --- |
| `Toggle` | booléen |
| `Dropdown` | chaîne |
| `MultiDropdown` | table de chaînes |
| `Slider` | nombre |
| `Keybind` | chaîne, `""` si aucune touche |
| `Input` | chaîne |
| `ColorPicker` | chaîne `#RRGGBBAA` |

## Ajouter un élément au registre à la main

```lua
Library:Register("mon_flag", {
    Type = "Toggle",
    Get = function() return monEtat end,
    Set = function(value) monEtat = value end,
})
```

Utile pour sauvegarder un état qui ne vient pas d'un élément de l'interface.

## Fonctions d'exécuteur utilisées

| Fonction | Usage | Absente ? |
| --- | --- | --- |
| `writefile`, `readfile`, `isfile` | configurations | repli mémoire |
| `listfiles`, `delfile` | liste et suppression | repli mémoire |
| `makefolder`, `isfolder` | arborescence | ignoré |
| `setclipboard`, `getclipboard` | copy / paste | boutons inactifs |
| `gethui`, `syn.protect_gui` | parentage du GUI | repli sur `CoreGui` puis `PlayerGui` |
| `game:HttpGet` | icônes Lucide | pas d'icônes |
