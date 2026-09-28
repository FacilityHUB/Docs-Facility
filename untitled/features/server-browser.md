# Server browser

Lists the public servers of a place, sorted by ping, with a join button on each
row.

```lua
local servers = Library:ServerBrowser()

section:Toggle({
    Text = "server browser",
    Flag = "server_browser",
    Callback = function(state) servers:SetVisible(state) end,
})
```

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Title` | string | `"servers"` | header |
| `Width` | number | `340` | width in pixels |
| `Height` | number | `420` | height in pixels |
| `Position` | UDim2 | centred | starting position |
| `MaxRows` | number | `40` | servers listed |
| `PlaceId` | number | current | place to list |
| `OnJoin` | function | – | replaces the default teleport |

## Methods

```lua
servers:SetVisible(true)
servers:Toggle()
servers:Refresh()
```

The first opening triggers a request on its own.

## Reading the list

Each row shows the player count, the ping and the server's average FPS. Ping
colours the line: green below 80 ms, yellow up to 150, red beyond. Rows are
sorted by ping, so the closest servers are on top.

The server you are currently in is left out when listing the current place.

## Another place

```lua
local servers = Library:ServerBrowser({
    PlaceId = 123456789,
})
```

Useful when a game has a separate lobby. From the lobby you can list and join
the game's servers directly.

## Games that refuse a direct teleport

Some games route every teleport through their own server and reject a client
call with error 773. In that case hand the join over to their module:

```lua
local servers = Library:ServerBrowser({
    PlaceId = 123456789,
    OnJoin = function(jobId, placeId, server)
        local Teleporter = require(game.ReplicatedStorage.Path.To.Teleporter)
        Teleporter.Request({ placeId = placeId, jobId = jobId })
    end,
})
```

`OnJoin` receives the chosen server's job id, the place id, and the full server
entry should you need its ping or player count.

Without `OnJoin` the browser calls `TeleportService:TeleportToPlaceInstance`,
which most games accept.

## Limits

The Roblox API returns no region information, which is why ping is shown
instead. A ping of 20 ms means a nearby server, 200 ms the other side of the
world.

The endpoint is rate limited, so refreshing every second will start failing. The
header shows `request failed` rather than erroring.
