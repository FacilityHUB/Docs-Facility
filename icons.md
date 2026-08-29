# Icons

Icons come from the Lucide library, ported to Roblox by Latte Softworks under the ISC license. The table is vendored in `addons/Icons.lua`: no third party repository is contacted at runtime.

Loading is deferred until the first icon is used, then cached — 145 KB that are never downloaded if you place no icons. To force it:

```lua
Library:PreloadIcons()
```

## Accepted formats

```lua
Icon = "alert-triangle"        -- Lucide name
Icon = 4483362458              -- asset id
Icon = "rbxassetid://4483362458"
```

A missing name, or a missing `Icons` addon, raises no error: the element simply renders without an icon.

## Where to use them

`Label`, `Paragraph` and notifications. The icon color follows the element style.

## Finding a name

Names vary between versions of `icons.lua` — `alert-triangle` versus `triangle-alert`, for instance. To list what is actually available:

```lua
for name in pairs(Library:PreloadIcons()["48px"]) do
    print(name)
end
```
