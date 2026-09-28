# Label

A line of text, usually to display a value that changes.

```lua
local status = section:Label("idle", { Style = "dim" })

status:Set("running")
status:SetStyle("success")
```

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Style` | string | `dim` | colour preset |
| `Color` | Color3 | – | explicit colour, wins over `Style` |
| `Icon` | string | – | Lucide icon on the left |
| `TextSize` | number | theme | overrides the size |
| `Font` | Font | theme | overrides the font |
| `KeepSpace` | boolean | `false` | keep the row when the text is empty |

## Methods

```lua
label:Set("new text")
label:SetColor(Color3.fromRGB(226, 102, 102))
label:SetStyle("danger")
```

## Empty labels

A label with empty text hides itself, so the card shrinks. That is what lets a
panel grow as data arrives instead of reserving space up front.

```lua
for i = 1, 10 do
    rows[i] = panel.Content:Label("")   -- nothing visible yet
end
```

Pass `KeepSpace = true` when a panel refreshes often and you would rather it
stayed a fixed height than jumped around.

## Live values

Keep the reference and call `:Set()` on a loop or an event:

```lua
local ping = section:Label("-", { Style = "success", Icon = "wifi" })

task.spawn(function()
    while task.wait(1) do
        local value = game:GetService("Stats").Network.ServerStatsItem["Data Ping"]
        ping:Set(math.floor(value:GetValue()) .. " ms")
    end
end)
```

For several values in columns, a [table](table.md) handles alignment for you.
