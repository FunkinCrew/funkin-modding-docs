# Creating an Album

## Album Assets

In order to create your own album, you will need 2 assets:

- `albumArtAsset`: The art that shows in Freeplay that represents the album itself.
- `albumTitleAsset`: The asset for the text that shows below the used album in Freeplay.

## Album Data

A custom album requires creating a new JSON file in the `data/ui/freeplay/albums` folder.

Below is the "volume1" album json file `assets/data/ui/freeplay/albums/volume1.json`[^albumsource]

```json
{
  "version": "1.0.0",
  "name": "Volume 1",
  "artists": ["Kawai Sprite"],
  "albumArtAsset": "freeplay/albumRoll/volume1",
  "albumTitleAsset": "freeplay/albumRoll/volume1-text"
}
```

While there is not a lot, some stuff still need to be shown so you know what is what!
- `version`: The version number for the Album data file format. Leave this at `1.0.0`.
- `name`: The readable name for the album.
- `artists:` The artists of the album, aka the ones who created the assets.
- `albumArtAsset`: The asset path to the album art which will be displayed in Freeplay.
- `albumTitleAsset`: The asset path to the album title which will be displayed below the album art in Freeplay.
- `albumTitleOffsets`: The global offset to the character's position, in pixels. Optional, defaults to `[0, 0]`.
  - Use an array of two decimal values, the first for horizontal position and the second for vertical position.
- `albumTitleAnimations`: A list of animation data objects for the album title. Optional, defaults to `[]`, aka nothing.

Animation data is structured like so:
- `name`: The internal animation name for the game to use.
- `prefix`: The animation name as specified by your spritesheet.
  - For Sparrow or Packer, check inside the data file to see what each set of frames is named, and use that as the prefix, excluding the frame numbers at the end.
  - For Animate Atlases, use either the frame label or the symbol name of the animation you want to play.
- `offsets`: Some animations may need their positions to be corrected relative to the idle animation.
  - Use an array of two decimal values, the first for horizontal position and the second for vertical position.
- `looped`: Whether to loop this animation in-game. If false, the animation will pause when it ends, until the game commands the asset to do something else.
- `flipX`: Whether to flip the sprites of this animation horizontally in-game.
- `flipY`: Whether to flip the sprites of this animation vertically in-game.
- `frameRate`: A frame rate value, defaulting to `24`.
- `frameIndices`: Optionally specify an array of frame numbers (starting at frame 0!) to use from a given prefix for this animation.
  - For example, specifying `[0, 1, 2, 3]` will make this animation only use the first 4 frames of the given prefix.

[^albumsource]: <https://github.com/FunkinCrew/funkin.assets/blob/main/preload/data/ui/freeplay/albums/volume1.json>