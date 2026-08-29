# Configurations

`Library.SaveManager` sérialise en JSON tous les éléments possédant un `Flag`.

## Mise en place

```lua
local SaveManager = Library.SaveManager

SaveManager:SetLibrary(Library)
SaveManager:IgnoreThemeSettings()      -- exclut les réglages d'interface
SaveManager:SetIgnoreIndexes({ "flag_a", "flag_b" })
SaveManager:SetFolder("Facility/mon-jeu")
SaveManager:BuildConfigSection(Settings, 2)
SaveManager:LoadAutoloadConfig()
```

`SetFolder` crée l'arborescence : `<dossier>/configs` et `<dossier>/settings`.

`BuildConfigSection` doit être appelé **après** la création de tous les éléments : il capture à ce moment les valeurs par défaut utilisées par `reset defaults`.

## Section générée

Champ `name`, liste `saved`, puis les actions : `save`, `load`, `delete`, `refresh`, `set autoload`, `clear autoload`, `copy`, `paste`, `reset defaults`. Deux libellés d'état affichent la configuration en autoload et la présence de modifications non enregistrées.

## API

```lua
SaveManager:Save("default")        -- écrit <dossier>/configs/default.json
SaveManager:Load("default.json")
SaveManager:Delete("default.json")
SaveManager:List()                 -- table de noms de fichiers
SaveManager:SetAutoload("default.json")
SaveManager:GetAutoload()
SaveManager:ClearAutoload()
SaveManager:LoadAutoloadConfig()
```

`Save` et `Load` retournent `ok, résultat` — le nom de fichier en cas de succès, un message d'erreur sinon.

## Autoload

Rien n'est chargé au démarrage tant qu'aucune configuration n'est marquée. `LoadAutoloadConfig` lit `<dossier>/settings/autoload.txt` et ne fait rien si le fichier est absent.

## Sans support fichier

Si l'exécuteur n'expose pas `writefile` / `readfile`, un stockage mémoire prend le relais : les boutons continuent de fonctionner, mais tout est perdu à la fin de la session.

## Contenu d'une configuration

```json
{
  "combat_enable": true,
  "combat_range": 25,
  "anchor": "head",
  "ignore": ["friends"],
  "inspect_key": "E",
  "highlight_color": "#E8A1A8FF"
}
```
