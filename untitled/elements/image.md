# Image

Displays an asset or a player's avatar.

```lua
local banner = section:Image({
    Image  = "rbxassetid://123456789",
    Height = 120,
})
```

## Options

| Option | Type | Default | Effect |
| --- | --- | --- | --- |
| `Image` | string | `""` | asset id or content string |
| `Height` | number | `120` | height in pixels, width fills the card |
| `Corner` | number | `6` | corner radius |
| `Border` | boolean | `true` | `false` removes the stroke |
| `ScaleType` | ScaleType | `Crop` | how the image fills the frame |
| `UserId` | number | – | loads that player's headshot |

## Methods

```lua
banner:Set("rbxassetid://987654321")
banner:SetHeight(160)
banner:SetUser(game.Players.LocalPlayer.UserId)
```

## Avatars

```lua
local avatar = section:Image({ Height = 96 })
avatar:SetUser(game.Players.LocalPlayer.UserId)
```

`SetUser` takes an optional thumbnail type and size:

```lua
avatar:SetUser(userId, Enum.ThumbnailType.AvatarBust, Enum.ThumbnailSize.Size420x420)
```

The image resolves through `rbxthumb`, which needs no API call and appears
immediately. A request is made in the background as a second attempt, so a
player who has just joined still gets their picture once it is available.

## Scale types

`Crop` fills the frame and cuts the overflow, which suits banners and avatars.
`Fit` shows the whole image with empty space around it, better for a logo whose
proportions must be kept.
