# Interface manager

`Library.InterfaceManager` construit la section de réglages de l'interface elle-même.

```lua
local InterfaceManager = Library.InterfaceManager

InterfaceManager:SetLibrary(Library)
InterfaceManager:SetWindow(Window)
InterfaceManager:SetFolder("Facility")
InterfaceManager:BuildInterfaceSection(Settings, 1)
```

## Contenu de la section

| Élément | Effet |
| --- | --- |
| `menu key` | raccourci d'ouverture, appliqué immédiatement |
| `ui scale` | échelle de 70 % à 130 % |
| `unload` | `Library:Destroy()` |

## Persistance

Aucune. Ces réglages vivent en mémoire pour la session et rien n'est écrit sur disque, donc rien ne s'applique tout seul au lancement suivant.

## Séparation avec les configurations

Les flags de cette section (`interface_menu_key`, `interface_scale`) sont listés dans `InterfaceManager.Flags`. `SaveManager:IgnoreThemeSettings()` les ajoute à la liste d'exclusion : ils ne sont ni sauvegardés, ni écrasés au chargement d'une configuration, et ne déclenchent pas l'indicateur de modifications non enregistrées.
