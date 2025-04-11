# Creating a new Sticker Pack

## Sticker Pack Assets

In order to create your own sticker pack, you will need graphics for the stickers you want to use. The ones included in the base game are generally around 300x300 in size, with some variation.

## Sticker Pack Data

A custom sticker pack requires creating a new JSON file in the `data/stickerpacks` folder.

Below is the "default" sticker pack JSON file `assets/data/stickerpacks/default.json`[^stickerpacksource]

```json
{
  "version": "1.0.0",
  "name": "Default",
  "artist": "PhantomArcade3K",
  "stickers": [
    "transitionSwag/stickers-set-1/bfSticker1",
    "transitionSwag/stickers-set-1/bfSticker2",
    "transitionSwag/stickers-set-1/bfSticker3"
  ]
}
```

Let's break it all down.
- `version`: The version number for the Sticker Pack data file format. Leave this at `1.0.0`.
  - This will increase if the data file format changes, and tell the game whether additional processing needs to be done for backwards compatibility.
- `name`: The readable name for the sticker pack, used in places like the Chart Editor.
- `author`: The author of the sticker pack, aka the artist who created the assets.
- `stickers`: A list of all the paths for all the stickers to use, as strings.
  - You cannot currently specify any additional arguments, such as scale, offsets, texture smoothing, or animations.

[^stickerpacksource]: <https://github.com/FunkinCrew/funkin.assets/blob/main/preload/data/stickerpacks/default.json>