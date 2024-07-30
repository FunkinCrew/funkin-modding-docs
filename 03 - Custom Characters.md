# Creating a Friday Night Funkin' Mod - Custom Characters

This guide will walk you through the process of creating a functioning, fully compatible Friday Night Funkin' mod, using the game's official systems for loading custom content and scripts. Once your mod is complete, you will be able to place it in the `mods` folder in your game install and use its content in-game without overriding the base game content and still maintain compatibility with other mods.

This entry goes over adding new characters to the game, and using them in a level.

## Character Assets

The individual sprites of a character's animations must be combined into a spritesheet for the game to use them. The game supports one of several formats:

- `sparrow`: Combines the images into a large sheet, then provides an XML file containing the coordinates of each frame with it. Can be exported directly from Adobe Animate using the `Generate Sprite Sheet` option, or can be created from individual frames using [Free Texture Packer](http://free-tex-packer.com/) (note that Free Texture Packer refers to this format as Starling).
- `packer`: Combines images into a sheet, then provides a TXT file containing the coordinates of each frame.
- `animateatlas`: Created exclusively when using Flash, this exports individual symbols into a large sheet, then provides a JSON file with data to split up each symbol, then provides a second JSON to arrange those symbols into animations. Great for performance, especially for characters which were made by rearranging smaller parts.
- `multisparrow`: Allows for different groups of animations to be exported into separate Sparrow spritesheets, then combined together into one character.

## Creating a Character

A custom character requires creating a new JSON file in the `data/characters` folder

```json
{
  "version": "1.0.0",
  "name": "Girlfriend",
  "renderType": "sparrow",
  "assetPath": "characters/GF_assets",
  "startingAnimation": "danceRight",
  "singTime": 8.0,
  "animations": [
    {
      "name": "danceLeft",
      "prefix": "GF Dancing Beat",
      "frameIndices": [30, 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14],
      "offsets": [0, -9]
    },
    {
      "name": "danceRight",
      "prefix": "GF Dancing Beat",
      "frameIndices": [
        15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29
      ],
      "offsets": [0, -9]
    },
    {
      "name": "sad",
      "prefix": "gf sad",
      "frameIndices": [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
      "offsets": [2, -21]
    },
    {
      "name": "singLEFT",
      "prefix": "GF left note",
      "offsets": [0, -19]
    },
    {
      "name": "singDOWN",
      "prefix": "GF Down Note",
      "offsets": [0, -20]
    },
    {
      "name": "singUP",
      "prefix": "GF Up Note",
      "offsets": [0, 4]
    },
    {
      "name": "singRIGHT",
      "prefix": "GF Right Note",
      "offsets": [0, -20]
    },
    {
      "name": "cheer",
      "prefix": "GF Cheer",
      "offsets": [0, 0]
    },
    {
      "name": "combo50",
      "prefix": "GF Cheer",
      "offsets": [0, 0]
    },
    {
      "name": "drop70",
      "prefix": "gf sad",
      "frameIndices": [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12],
      "offsets": [2, -21]
    },
    {
      "name": "hairBlow",
      "prefix": "GF Dancing Beat Hair blowing",
      "frameIndices": [0, 1, 2, 3],
      "offsets": [45, -8]
    },
    {
      "name": "hairFall",
      "prefix": "GF Dancing Beat Hair Landing",
      "frameIndices": [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11],
      "offsets": [0, -9]
    },
    {
      "name": "scared",
      "prefix": "GF FEAR",
      "offsets": [-2, -17]
    }
  ]
}
```

The available fields are:
- `version`: The version number for the Character data file format. Leave this at `1.0.0`.
- `name`: The readable name for the character, used in places like the Chart Editor.
- `renderType`: The render type. One of `sparrow`, `packer`, `animateatlas`, `multisparrow`.
- `assetPath`: The main asset path to use for this character, relative to the `images` directory in your mod folder.
  - For the `sparrow` asset type, this must point to the path where the `xml` and `png` are located, without the file extension.
  - For the `packer` asset type, this must point to the path where the `txt` and `png` are located, without the file extension.
  - For the `animateatlas` asset type, this must point to the folder where the `Animation.json` and any spritemaps are located.
  - For the `multisparrow` asset type, point to the path where your main Sparrow spritesheet is located. On each animations which uses a different Sparrow spritesheet from the main one, add the `assetPath` key to that specific animation.
- `startingAnimation`: The animation for the character to play when they are first loaded in.
- `singTime`: The amount of time, in steps, for a character to keep singing after they let go of a note.
  - Decrease this if the character seems to hold their poses for too long after their section is done.
  - Increase this if the character resets to the idle animation in the middle of their singing animations.
- `animations`: A list of animation data objects for the character.

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

## Replacing/Reskinning an Existing Character

As a short aside, you can create a JSON with the same filename as an existing character (from the base game, or from a mod if your mod loads after it) and it will replace it. This can be used to create more elaborate reskins for characters, such as ones that use a different render type.

## Using a Character in a Song

There are two ways to use your character in a song once it's implemented.

1. Create a new chart. Open the Chart Editor, start a chart, and select the character from the `Metadata` toolbox before charting.
2. Edit an existing chart in your mod. Open the `metadata.json` file and check in `playData.characters` for the `player`, `girlfriend`, and `opponent` keys.

Once the chart which references your character is in your mod folder, simply start the game with your mod installed.
