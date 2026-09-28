# Troubleshooting

## A change does not show up

The host is serving a cached copy.

```lua
print(Library.Version)
```

If that is not the build you pushed, wait a few minutes or force a fresh copy
with `?v=` .. `tick()` as described in [Hosting](hosting.md).

## `attempt to index nil with ...` on a manager

`Library.BaseUrl` is wrong, or the file is not where the path says. The library
loads, the manager is `nil`, and the error only appears on first use.

Open the addon URL in a browser to confirm it serves the right file. A repository
where two files were swapped gives exactly this.

## A section is missing

An error during the build stops everything after it in the same tab. Look for
the first error in the console rather than the missing section: the cause is
usually above.

## The theme only applies partly

Call `ThemeManager:Load()` as the last line of the script. Earlier, it repaints
an interface that is not built yet.

## Something disappears when a modal opens

A colour that is not meant to follow the theme has to opt out with
`ThemeTag = { BackgroundColor3 = false }`. Otherwise a value matching a palette
colour gets recoloured and can inherit an alpha.

## The key prompt never appears

A key was saved on a previous run.

```lua
if isfile("FacilityKey.dat") then delfile("FacilityKey.dat") end
```

Or set `SaveKey = false` while testing.

## Error 773 when joining a server

The game routes teleports through its own server and refuses a client call. Use
`OnJoin` to go through the game's own module, see
[Server browser](server-browser.md).

## Configs do not come back

Nothing is restored unless a config is marked for autoload. Use the `set
autoload` button, or call `SaveManager:Load("name.json")` explicitly.

## Saving does nothing

The executor lacks `writefile` and friends. The interface still works, saving
does not.

```lua
print(writefile ~= nil, readfile ~= nil, isfile ~= nil, listfiles ~= nil)
```

## Two elements share a flag

The console warns and the second one wins. Prefix flags by feature.
