# Key system

Blocks the script until a valid key is entered. The window is not built until
then, so nothing of the interface shows behind the prompt.

```lua
local Window = Library:Window({
    Title  = "facility",
    Suffix = ".app",

    KeySystem = true,
    KeySettings = {
        Title    = "Facility",
        Subtitle = "Enter your key to continue",
        Note     = "Get your key on our Discord",
        FileName = "FacilityKey",
        SaveKey  = true,
        Key      = { "FACILITY-2024", "FACILITY-BETA" },
    },
})
```

## Settings

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Title` | string | `"Key System"` | header, left side |
| `Subtitle` | string | – | line under the title |
| `Note` | string | – | text on the right, supports rich text |
| `FileName` | string | `"key"` | file the key is saved to |
| `SaveKey` | boolean | `true` | skip the prompt once validated |
| `GrabKeyFromSite` | boolean | `false` | `Key` holds URLs instead of strings |
| `Key` | table | `{}` | accepted keys, or URLs |
| `GetKey` | string | – | link copied by the Get-Key button |
| `Discord` | string | – | invite code for the Discord button |

## Buttons

`GetKey` and `Discord` each add their own button on the right side. Leave one
out and it is not drawn; leave both out and only the note shows.

## Remote keys

```lua
KeySettings = {
    GrabKeyFromSite = true,
    Key = { "https://pastebin.com/raw/xxxxxxx" },
}
```

Every entry is fetched and read line by line, so a paste holding one key per line
works and can be rotated without touching the script.

## Saved keys

With `SaveKey = true` a validated key is written next to the executor and read
back on the next run. If it is still in the accepted list the prompt does not
appear.

While testing, that means the prompt shows once and never again. Delete the file
to see it again:

```lua
if isfile("FacilityKey.dat") then delfile("FacilityKey.dat") end
```

## Appearance

The prompt uses the saved theme, read before anything is drawn, so it matches
the interface that follows. It is draggable and has no logo.
