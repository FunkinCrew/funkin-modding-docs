# Creating a Playable Character

A custom playable character requires creating a new JSON file in the `data/characters` folder. Below is an example of Pico's character data file, from `assets/data/players/pico.json`[^picosource]

```json
{
  "version": "1.0.0",
  "name": "Pico",
  "ownedChars": [
    "pico",
    "pico-playable",
    "pico-blazin",
    "pico-christmas",
    "pico-dark"
  ],
  "showUnownedChars": false,
  "unlocked": true,
  "freeplayStyle": "pico",
  "freeplayDJ": {
    "assetPath": "freeplay/freeplay-pico",
    "text1": "PICO",
    "text2": "GOD DAMN HE DOWN ON THE NUT",
    "text3": "ZEBOIM DAMN IMA NUT",
    "fistPump": {
      "introStartFrame": 0,
      "introEndFrame": 4,

      "loopStartFrame": 4,
      "loopEndFrame": -1,

      "introBadStartFrame": 0,
      "introBadEndFrame": 0,

      "loopBadStartFrame": 0,
      "loopBadEndFrame": -1
    },
    "charSelect": {
      "transitionDelay": 0.45
    },
    "animations": [
      {
        "name": "intro",
        "prefix": "pico dj intro",
        "offsets": [631.7, 362.6]
      },
      {
        "name": "idle",
        "prefix": "Pico DJ",
        "offsets": [625, 360]
      },
      {
        "name": "idleEasterEgg",
        "prefix": "Pico DJ afk",
        "offsets": [625, 360]
      },
      {
        "name": "confirm",
        "prefix": "Pico DJ confirm",
        "offsets": [625, 360]
      },
      {
        "name": "fistPump",
        "prefix": "pico cheer",
        "offsets": [975, 260]
      },
      {
        "name": "loss",
        "prefix": "Pico DJ loss",
        "offsets": [625, 360]
      },
      {
        "name": "charSelect",
        "prefix": "Pico DJ to CS",
        "offsets": [625, 360]
      }
    ]
  },
  "charSelect": {
    "position": 3,
    "gf": {
      "assetPath": "charSelect/neneChill",
      "animInfoPath": "charSelect/neneAnimInfo",
      "visualizer": true
    }
  },
  "results": {
    "music": {
      "PERFECT_GOLD": "resultsPERFECT-pico",
      "PERFECT": "resultsPERFECT-pico",
      "EXCELLENT": "resultsEXCELLENT-pico",
      "GREAT": "resultsNORMAL-pico",
      "GOOD": "resultsNORMAL-pico",
      "SHIT": "resultsSHIT-pico"
    },
    "perfectGold": [
      {
        "renderType": "animateatlas",
        "assetPath": "shared:resultScreen/results-pico/resultsPERFECT",
        "zIndex": 500,
        "scale": 0.88,
        "offsets": [385, 82],
        "loopFrame": 91
      }
    ],
    "perfect": [
      {
        "renderType": "animateatlas",
        "assetPath": "shared:resultScreen/results-pico/resultsPERFECT",
        "zIndex": 500,
        "scale": 0.88,
        "offsets": [385, 82],
        "loopFrame": 91
      }
    ],
    "excellent": [
      {
        "renderType": "animateatlas",
        "assetPath": "shared:resultScreen/results-pico/resultsGREAT",
        "zIndex": 500,
        "scale": 1.25,
        "offsets": [350, 25],
        "looped": true,
        "loopFrame": 32
      }
    ],
    "great": [
      {
        "renderType": "animateatlas",
        "assetPath": "shared:resultScreen/results-pico/resultsGREAT",
        "zIndex": 500,
        "scale": 1.25,
        "offsets": [350, 25],
        "looped": true,
        "loopFrame": 32
      }
    ],
    "good": [
      {
        "renderType": "animateatlas",
        "assetPath": "shared:resultScreen/results-pico/resultsGOOD",
        "zIndex": 500,
        "scale": 1.25,
        "offsets": [350, 25],
        "loopFrame": 41
      }
    ],
    "loss": [
      {
        "renderType": "animateatlas",
        "assetPath": "shared:resultScreen/results-pico/resultsSHIT",
        "zIndex": 500,
        "offsets": [-185, -125],
        "loopFrame": 0
      }
    ]
  }
}
```

The available fields are:
- `version`: The version number for the Playable Character data file format. Leave this at `1.0.0`.
- `name`: The readable name for the character, used internally.
- `ownedCharacters`: The list of [Characters](../03-custom-characters/03-00-custom-characters.md) this character owns.
    - When determining which songs to display in Freeplay, the game checks for any songs where the player character is in this list and displays those. Songs where the player character is in another array are not displayed.
- `showUnownedChars`: If this value is `true`, then songs whose player character is not in any `ownedCharacters` list will be displayed for this character.
- `unlocked`: Whether the character is unlocked.
    - Create a scripted class for this playable character and override `isUnlocked():Bool` to make this conditional. See [Scripted Playable Characters](21-scripted-classes\21-10-scripted-playable-characters.md)
- `freeplayStyle`: The ID for a Freeplay style to display.
    - You can use `"bf"` here to use Boyfriend's Freeplay style as a default, or create a new JSON file in the `data/ui/freeplay/styles` folder (copy the Pico one and edit that).
- `freeplayDJ`: Data for how the character displays as the DJ in the Freeplay menu.
- `charSelect`: Data for how the character displays in the Character Select menu.
- `results`: Data for how the character displays in the Results screen.

Freeplay DJ data is structured like so:
- `assetPath`: The folder where the Animate Atlas for this character is located, relative to the `images/` folder.
    - Note that Sparrow atlases are not supported for Freeplay animations.
- `animations`: A list of animation data for the character.
    - Valid animation names include `intro` `idle` `idleEasterEgg` `confirm` `fistPump` `loss` `charSelect` and `
- `charSelect`: A structured data object containing:
    - `transitionDelay`: A duration (in seconds) between when the character's transition to Character Select starts and the camera starts to fade.
- `fistPump`: A structured data object containing:
    - `introStartFrame` The frame number in the `fistPump` animation where the intro animation (which loops until the rank slams down) starts.
    - `introEndFrame` The frame number in the `fistPump` animation where the intro animation ends.
    - `loopStartFrame` The frame number in the `fistPump` animation where the follow-up animation starts.
    - `loopEndFrame` The frame number in the `fistPump` animation where the follow-up animation ends.
        - Use `-1` to use the last frame of the specified frame label.
    - `introBadStartFrame` The frame number in the `loss` animation where the intro animation starts.
    - `introBadEndFrame` The frame number in the `loss` animation where the intro animation ends.
    - `loopBadStartFrame` The frame number in the `loss` animation where the follow-up animation starts.
    - `loopBadEndFrame` The frame number in the `loss` animation where the follow-up animation ends.

Character Select data is structured like so:
- `position`: The preferred grid square for the character in the Character Select grid.
    - `0` represents the top left, `3` represents the middle left, and `8` represents the bottom right.
    - Characters are evaluated alphabetically, and if the slot is already occupied, they will be shifted over until they fit.
    - At time of writing (v0.5.1) only 9 total characters can fit in the grid.
- `gf`: (NEW with v0.5.1) A structured data object containing:
    - `assetPath`: The folder where the Animate Atlas for this character is located, relative to the `images/` folder.
        - Note that Sparrow atlases are not supported.
    - `animInfoPath`: A path to a Flash JSFL file describing character sliding movement.
    - `visualizer`: Whether the character is hooked up to display a visualizer (like Nene's ABot).
        - Check the Nene Character Select FLA to see how to implement this.

Results data is structured like so:
- `music`: A structured data object containing:
    - `PERFECT_GOLD`: The path to a music track in the `music/` folder. Played during the Perfect rank animation with all SICKs.
    - `PERFECT`: The path to a music track in the `music/` folder. Played during the Perfect rank animation.
    - `EXCELLENT`: The path to a music track in the `music/` folder. Played during the Excellent rank animation.
    - `GREAT`: The path to a music track in the `music/` folder. Played during the Great rank animation.
    - `GOOD`: The path to a music track in the `music/` folder. Played during the Good rank animation.
    - `SHIT`: The path to a music track in the `music/` folder. Played during the Loss rank animation.
    - Make sure to include a metadata file in the folder to tell the game what BPM the song is, and how to loop it.
    - Include a variation of the track with the suffix `-intro.ogg` to play that track once before playing the main music track.
- `perfect`: An array of animation data structures, describing the animation played when the player gets a Perfect rank.
    - Data is in the form of an array of animation objects.
    - You can use Sparrow animations or `animateatlas` sprites. Use `renderType` to tell the game which one to use.
    - Use `loopFrame` to tell the game which frame to start looping at, or set `looped` to `"false"` to just play the animation once.
- `excellent`: Data for the animation played when the player gets a Excellent rank.
- `great`: Data for the animation played when the player gets a Great rank.
- `good`: Data for the animation played when the player gets a Good rank.
- `loss`: Data for the animation played when the player gets a Loss rank.
- `perfectGold`: (NEW with v0.5.1) Data for the animation played when the player gets a Perfect rank with all SICKs.
    - In the base game, this is just the same data as `perfect`, but you can make it different if you like.

[^picosource]: <https://github.com/FunkinCrew/funkin.assets/blob/main/preload/data/players/pico.json>