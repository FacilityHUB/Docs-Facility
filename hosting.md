# Hosting

## File layout

Every file must sit at the exact path declared in `AddonPaths`, relative to
`Library.BaseUrl`:

```
main.luau
addons/Icons.luau
addons/SaveManager.luau
addons/InterfaceManager.luau
addons/ThemeManager.luau
```

```lua
Library.BaseUrl = "https://raw.githubusercontent.com/user/repo/refs/heads/main/"
```

Open the full URL of one addon in a browser to confirm it serves raw code before
shipping. A wrong base URL is silent: the library still loads, but
`Library.SaveManager` is `nil` and only fails on first use.

## Caching

Raw file hosts cache aggressively, often for minutes. A change pushed to the
repository does not appear right away.

```lua
print(Library.Version)
```

That tells you which build is really running. While testing, force a fresh copy:

```lua
local source = game:HttpGet(BASE .. "main.luau?v=" .. tostring(tick()))
local Library = loadstring(source)()
```

Remove it before shipping: it defeats caching entirely and costs a full download
on every run.

## Checking a load

```lua
local source = game:HttpGet(BASE .. "main.luau")
assert(#source > 1000, "main.luau not found at this URL")

local chunk, err = loadstring(source)
assert(chunk, "main.luau does not compile: " .. tostring(err))

local Library = chunk()
assert(type(Library) == "table", "main.luau returned nothing")
```

Worth keeping in a published script. A truncated or misplaced file then gives a
clear message instead of a confusing error later on.

## Where the interface lives

`gethui()` first, then `syn.protect_gui`, then `CoreGui`, then `PlayerGui`,
taking the first that works.

Every `ScreenGui` gets a random twelve character name at each run and the
maximum `DisplayOrder`, so nothing is identifiable by a fixed name.

Roblox automatically translates a few common words, which turned "Settings" into
its localised form. `AutoLocalize` is disabled on every `ScreenGui` to stop
that.

## Global handle

```lua
print(getgenv().Facility.Version)
print(getgenv().Facility.Flags)
```

Handy when debugging from a second script, since `Library` is local to yours.
