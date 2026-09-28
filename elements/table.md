# Table

Read only rows with aligned columns.

```lua
local board = section:Table({
    Columns   = { "unit", "level", "cooldown" },
    MaxRows   = 10,
    EmptyText = "nothing placed",
})

board:SetRows({
    { "Yammy",    "3", "ready" },
    { "Espada 6", "1", "12s" },
})
```

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Columns` | table | `{ "column" }` | header names, also sets the column count |
| `MaxRows` | number | `12` | rows allocated once at creation |
| `RowHeight` | number | `18` | row height in pixels |
| `Header` | boolean | `true` | `false` removes the header line |
| `AlignRight` | boolean | `false` | right aligns every column but the first |
| `EmptyText` | string | `"no data"` | shown when there is nothing |
| `KeepHeader` | boolean | `false` | keep the header visible when empty |
| `Rows` | table | – | initial content |

## Methods

```lua
board:SetRows({ { "a", "1", "x" } })   -- returns how many rows were shown
board:Clear()
```

Rows are allocated once when the table is created, so `SetRows` creates no
instances. It is safe to call every frame or on a tight loop.

Rows beyond `MaxRows` are ignored, so size it for the worst case.

## Colouring rows

```lua
board:SetRows({
    { "Yammy", "3", "ready", Style = "success" },
    { "Hollow", "1", "12s", Colors = { nil, nil, Color3.fromRGB(226, 102, 102) } },
})
```

`Style` colours the whole row, `Colors` one cell at a time with `nil` leaving a
cell untouched.

## A live example

```lua
local roster = section:Table({
    Columns = { "player", "distance" },
    MaxRows = 8,
    EmptyText = "nobody nearby",
})

task.spawn(function()
    while task.wait(1) do
        local rows = {}
        local me = game.Players.LocalPlayer.Character
        local myRoot = me and me:FindFirstChild("HumanoidRootPart")

        for _, other in ipairs(game.Players:GetPlayers()) do
            if other ~= game.Players.LocalPlayer and #rows < 8 then
                local char = other.Character
                local root = char and char:FindFirstChild("HumanoidRootPart")
                local distance = "-"
                if myRoot and root then
                    distance = string.format("%dm", (myRoot.Position - root.Position).Magnitude)
                end
                table.insert(rows, { other.DisplayName, distance })
            end
        end

        roster:SetRows(rows)
    end
end)
```

Three or four columns is the practical limit in a side column; use a
[full width band](../sections.md) beyond that.
