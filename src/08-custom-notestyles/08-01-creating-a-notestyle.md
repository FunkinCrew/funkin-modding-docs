# Creating a Note Style

## Note Style Assets

In order to create your own note style, you will need up to 4 assets:
1. `notes`
2. `noteStrumline`
3. *OPTIONAL* `noteSplashes` *(CURRENTLY DOESN'T WORK)*
4. *OPTIONAL* `holdCover` *(CURRENTLY DOESN'T WORK)*

## Note Style Data

A custom stage requires creating a new JSON file in the `data/notestyles` folder

Below is the "funkin" (aka the default used everywhere) json file `assets/data/notestyles/funkin.json`[^notestylesource]

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
- `author`:
- `fallback`:
- `assets`: A list of assets data for the note style.
    - See [list of asset data](#note-style-assets) that can be used.

Asset data is structured like so:
- `assetPath`: The main asset path to use for this asset.
- `scale`: Specify the size of the asset relative to the original size. For example, `2.0` makes the sprite twice as big. Defaults to `1.0` if unspecified.
- `offsets`: Some animations may need their positions to be corrected relative to the idle animation.
  - Use an array of two decimal values, the first for horizontal position and the second for vertical position.
- `isPixel`: Specify whether to display this asset as being pixel (disabling texture smoothing). Optional, defaults to `false`.
- `data`: The structure of animation data objects that depends on the asset you are going to edit.

Animation data is structured like so:
- `note`:
  - ``
- `noteStrumline`:
- `holdNote`:
- `noteSplash`
  - `enabled`: Specify whether to display this asset. Optional, defaults to `true`.
- `holdNoteCover`
  - `enabled`: Specify whether to display this asset. Optional, defaults to `true`.

Animation data is structured like so:
- `prefix`: The animation name as specified by your spritesheet.
  - For Sparrow or Packer, check inside the data file to see what each set of frames is named, and use that as the prefix, excluding the frame numbers at the end.
  - For Animate Atlases, use either the frame label or the symbol name of the animation you want to play.
- `offsets`: Some animations may need their positions to be corrected relative to the idle animation.
  - Use an array of two decimal values, the first for horizontal position and the second for vertical position.
- `looped`: Whether to loop this animation in-game. If false, the animation will pause when it ends, until the game commands the character to do something else.
- `flipX`: Whether to flip the sprites of this animation horizontally in-game.
- `flipY`: Whether to flip the sprites of this animation vertically in-game.
- `frameRate`: A frame rate value, defaulting to `24`.
- `frameIndices`: Optionally specify an array of frame numbers (starting at frame 0!) to use from a given prefix for this animation.
  - For example, specifying `[0, 1, 2, 3]` will make this animation only use the first 4 frames of the given prefix.
- `assetPath`: For the `multisparrow` asset type specifically. Define a secondary Sparrow spritesheet which will be loaded, and which contains the frames for this animation.

[^notestylesource]: <https://github.com/FunkinCrew/funkin.assets/blob/main/preload/data/notestyles/funkin.json>