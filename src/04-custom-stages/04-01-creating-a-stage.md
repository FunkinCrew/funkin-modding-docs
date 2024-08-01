# Creating a Stage

## Stage Assets

The image assets required for a stage should be placed into the `shared/images/` folder within your mod, ideally somewhere organized like a subfolder with the name of the stage.

## Stage Data

A custom stage requires creating a new JSON file in the `data/stages` folder

Below is the "Main Stage" json file from Week 1 `assets/data/stages/mainStage.json`[^stagesource]

```json
{
  "version": "1.0.1",
  "name": "Main Stage",
  "cameraZoom": 1.1,
  "props": [
    {
      "zIndex": 10,
      "position": [-600, -200],
      "scale": [1, 1],
      "name": "stageBack",
      "assetPath": "stages/mainStage/stageback",
      "scroll": [0.9, 0.9]
    },
    {
      "zIndex": 20,
      "position": [-650, 600],
      "scale": [1.1, 1.1],
      "name": "stageFront",
      "assetPath": "stages/mainStage/stagefront",
      "scroll": [0.9, 0.9]
    },
    {
      "zIndex": 30,
      "position": [-500, -300],
      "scale": [0.9, 0.9],
      "name": "stageCurtains",
      "assetPath": "stages/mainStage/stagecurtains",
      "scroll": [1.3, 1.3]
    }
  ],
  "characters": {
    "bf": {
      "zIndex": 300,
      "position": [989.5, 885],
      "cameraOffsets": [-100, -100]
    },
    "dad": {
      "zIndex": 200,
      "position": [335, 885],
      "cameraOffsets": [150, -100]
    },
    "gf": {
      "zIndex": 100,
      "cameraOffsets": [0, 0],
      "position": [751.5, 787]
    }
  }
}

```

The available fields are:
- `version`: The version number for the Stage data file format. Leave this at `1.0.1`.
- `name`: The readable name for the stage, used in places like the Chart Editor.
- `cameraZoom`: The default camera zoom level for the stage. Optional, defaults to `1.0`.
- `props`: An array of props to add to the stage, specifying what sprites should be used and where those sprites should be positioned.
- `characters`: Data on how characters in the stage should be positioned.

Stage prop data is structured like so:
- `name`: An internal name for this prop. Good for keeping track of things. Keep each prop name unique!
  - You can access a stage prop in a script using `PlayState.instance.currentStage.getNamedProp(name)`.
- `assetPath`: The asset used to display the prop. This can be either an image or a color.
  - To use an image, specify the path relative to the `images` folder in your mod folder.
  - To use a color, specify a hex code. This creates a 1x1 pixel square of the specified color, which you can resize with the `scale` property.
- `zIndex`: A value describing the relative position of the prop. Optional, defaults to `0`.
  - Elements with higher values get placed in front of elements with lower values.
- `position`: The horizontal and vertical position of the prop, in pixels.
- `isPixel`: Specify whether to display this image as a pixel prop (disabling texture smoothing). Optional, defaults to `false`.
- `scale`: Specify the size of the prop relative to the original size. For example, `2.0` makes the sprite twice as big. Defaults to `1.0` if unspecified.
- `alpha`: Specify the opacity of the prop, with `1.0` being fully opaque and `0.0` being completely transparent. Optional, defaults to `1.0`.
- `scroll`: Specify how much scroll factor, or how much the prop moves relative to the camera horizontally and vertically. Defaults to `[0.0, 0.0]` if unspecified.
  - A value of `[0, 0]` causes the prop to not move at all in relation to the camera.
  - A value of `[1, 1]` causes the prop to move 1-to-1 with the camera. Characters usually have a scroll factor of `[1, 1]`.
  - A value of `[0, 1]` causes the prop to only move vertically in relation to the camera as focus changes.
  - A value of `[0.5, 0.5]` causes the prop to move less relative to props configured to move 1-to-1
  - A value of `[2, 2]` is valid and causes the prop to move 2-to-1 as the camera moves.
- `animType`: If the prop you choose is animated, specify `sparrow` or `packer` for which animation type you're using.
  - Most of the game's spritesheets are Sparrow v2 sheets exported from Adobe Animate.
- `animations`: A list of animation data objects for the stage prop.
- `startingAnimation`: The animation to play on the prop when the stage starts. If the animation is configured to loop, it will play forever unless a script calls a different one (or `danceEvery` is greater than 0). If unspecified, no animation will play unless a script does so.
- `danceEvery`: If non-zero, this prop will play an animation every X beats of the song. Defaults to `0.0`, or no bopping.
  - This tries to play the `idle` animation.
  - If `danceLeft` and `danceRight ` animations are specified, the game will alternate between these instead.
  - This value supports precision up to `0.25`, where `0.25` plays the animation four times per beat.

Stage prop animation data is structured like so:
- `name`: The internal animation name for the game to use.
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

Character data is structured like so:
- `bf`: Data about the stage's player character.
  - `zIndex`: A value describing the relative position of the player character. Elements with higher values get placed in front of those with lower values.
  - `position`: The X and Y position where the character should be positioned, relative to other props in the stage.
  - `scale`: The relative scale to display the character at. For example, `0.5` makes the character half as big as the default.
  - `cameraOffsets`: When the camera focuses on this character, focus on the character's center, then apply camera offsets to shift the camera focus to the desired spot.
- `dad`: Data about the stage's opponent character.
  - `zIndex`: A value describing the relative position of the opponent character. Elements with higher values get placed in front of those with lower values.
  - `position`: The X and Y position where the character should be positioned, relative to other props in the stage.
  - `scale`: The relative scale to display the character at. For example, `0.5` makes the character half as big as the default.
  - `cameraOffsets`: When the camera focuses on this character, focus on the character's center, then apply camera offsets to shift the camera focus to the desired spot.
- `gf`: Data about the stage's background character.
  - `zIndex`: A value describing the relative position of the background character. Elements with higher values get placed in front of those with lower values.
  - `position`: The X and Y position where the character should be positioned, relative to other props in the stage.
  - `scale`: The relative scale to display the character at. For example, `0.5` makes the character half as big as the default.
  - `cameraOffsets`: When the camera focuses on this character, focus on the character's center, then apply camera offsets to shift the camera focus to the desired spot.


Animation data is structured like so:
- `name`: The internal animation name for the game to use.
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

The animation names the game uses by default are:
- `idle`: For the idle animation.
- `danceLeft` and `danceRight`: Supercedes the idle animation with one that toggles between two animations.
- `singLEFT`, `singDOWN`, `singUP`, `singRIGHT`: The animations for playing notes, when the character is a player or opponent.
- `singLEFTmiss`, `singDOWNmiss`, `singUPmiss`, `singRIGHTmiss`: The animations for missing notes, when the character is a player.
- Adding a new singing animation with the name of an existing animation with `-hold` at the end will play the animation after the first one ends, while the character is still singing.
  - As a good example, you can copy the `singLEFT` animation to make a `singLEFT-hold` animation, which has `looped` as true and `frameIndices` as the last few frames of the singing animation.
- Adding a new singing animation with the name of an existing animation with `-end` at the end will play an animation before returning to idle.
  - For example, you can define a new `singLEFT-end` animation to cleanly transition into the idle animation.
- You can add other animations by name, but you'll have to play them with a script, or a `Play Animation` song event in the Chart Editor.

When the game starts, it queries the list of possible characters by searching in the `data/characters` folder for JSON files. This gets used to preload data which is used later when the character is loaded in a stage.

[^stagesource]: <https://github.com/FunkinCrew/funkin.assets/blob/main/preload/data/stages/mainStage.json>
