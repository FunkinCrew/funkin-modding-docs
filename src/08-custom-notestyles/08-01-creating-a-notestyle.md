# Creating a Note Style

## Note Style Assets

In order to create your own note style, you will need up to 4 assets:
- `notes`: The general notes that are displayed in the chart, as well as in-game the player needs to hit.
- `noteStrumline`: The notes on the strumline, along with their corresponding animations, such as it being `static`, the strumline note being `pressed`, `confirming` the note hit.
- `noteSplashes`: The special effect when the player gets `Sick!` rating.
  - Currently is buggy, since it doesn't use the asset you provided.
- `holdCover`: The special effect when the player is holding a note.
  - Currently is buggy, since it doesn't use the asset you provided.

## Note Style Data

A custom note style requires creating a new JSON file in the `data/notestyles` folder.

Below is the "funkin" (aka the default) note style json file `assets/data/notestyles/funkin.json`[^notestylesource]

```json
{
  "version": "1.0.0",
  "name": "Funkin'",
  "author": "PhantomArcade",
  "fallback": null,
  "assets": {
    "note": {
      "assetPath": "shared:notes",
      "scale": 1.0,
      "data": {
        "left": { "prefix": "noteLeft" },
        "down": { "prefix": "noteDown" },
        "up": { "prefix": "noteUp" },
        "right": { "prefix": "noteRight" }
      }
    },
    "noteStrumline": {
      "assetPath": "shared:noteStrumline",
      "scale": 1.55,
      "offsets": [0, 0],
      "data": {
        "leftStatic": { "prefix": "staticLeft0" },
        "leftPress": { "prefix": "pressLeft0" },
        "leftConfirm": { "prefix": "confirmLeft0" },
        "leftConfirmHold": { "prefix": "confirmLeft0" },
        "downStatic": { "prefix": "staticDown0" },
        "downPress": { "prefix": "pressDown0" },
        "downConfirm": { "prefix": "confirmDown0" },
        "downConfirmHold": { "prefix": "confirmDown0" },
        "upStatic": { "prefix": "staticUp0" },
        "upPress": { "prefix": "pressUp0" },
        "upConfirm": { "prefix": "confirmUp0" },
        "upConfirmHold": { "prefix": "confirmUp0" },
        "rightStatic": { "prefix": "staticRight0" },
        "rightPress": { "prefix": "pressRight0" },
        "rightConfirm": { "prefix": "confirmRight0" },
        "rightConfirmHold": { "prefix": "confirmRight0" }
      }
    },
    "holdNote": {
      "assetPath": "NOTE_hold_assets",
      "data": {}
    },
    "noteSplash": {
      "assetPath": "",
      "data": {
        "enabled": true
      }
    },
    "holdNoteCover": {
      "assetPath": "",
      "data": {
        "enabled": true
      }
    }
  }
}
```

There is quite a lot to unravel, let's break it all down.
- `version`: The version number for the Note Style data file format. Leave this at `1.0.0`.
- `name`: The readable name for the note style, used in places like the Chart Editor.
- `author`: The author of the note style, aka the artist who created the assets.
- `fallback`: The note style to use as a fallback/parent, providing a default option when the note style you are using is not available. Optional, defaults to `null`.
- `assets`: A list of asset data for each of the assets for the note style.
    - See [list of assets](#note-style-assets) that you can provide the data for.

Asset data is structured like so:
- `assetPath`: The main asset path to use for this asset.
- `scale`: Specify the size of the asset relative to the original size. For example, `2.0` makes the sprite twice as big. Defaults to `1.0` if unspecified.
- `offsets`: Some animations may need their positions to be corrected relative to the idle animation.
  - Use an array of two decimal values, the first for horizontal position and the second for vertical position.
- `isPixel`: Specify whether to display this asset as being pixel (disabling texture smoothing). Optional, defaults to `false`.
- `data`: The structure of note style asset data objects that depends on the asset you are going to edit.

Note Style Asset data is structured like so:
- For `note`: List of animation data for the `left`, `down`, `up` and `right` arrows.
- For `noteStrumline`: List of animation data for each direction and it's variations, such as `<direction>Static`, `<direction>Press`, `<direction>Confirm`, `<direction>ConfirmHold` replacing `<direction>` with it's each and every corresponding direction.
  - As you may see from the [example](#note-style-data)[^notestylesource] that was given, animation data for the `confirm` and `confirmHold` match up, however you can make it have unique animations.
- For `holdNote`: Currently has no list of animation data that can be set.
- For `noteSplash`: There is currently no list of animation data available that can be set. It is likely to be added in the future.
  - `enabled`: Specify whether to display the asset. Optional, defaults to `true`.
- For `holdNoteCover`: There is currently no list of animation data available that can be set. It is likely to be added in the future.
  - `enabled`: Specify whether to display the asset. Optional, defaults to `true`.

Animation data is structured like so:
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

[^notestylesource]: <https://github.com/FunkinCrew/funkin.assets/blob/main/preload/data/notestyles/funkin.json>