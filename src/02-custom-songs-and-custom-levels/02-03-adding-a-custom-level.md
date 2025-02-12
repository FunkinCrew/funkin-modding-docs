# Adding a Custom Level

Add a new file, with whatever internal name you like, into your mods folder, under the `data/levels/` directory, with the `.json` file extension.

*NOTE*: Keep in mind that if your internal name is the same as a week from the base game, or of another mod, they will overlap each other and you may have unexpected results!

We'll end up with something like this.

```
-mods
 |-myMod
   |-data
     |-levels
       |-myweek.json
     |-songs
       |-mychart
         |-mychart-metadata.json
         |-mychart-chart.json
   |-songs
     |-mychart
       |-Inst.ogg
       |-Voices-bf.ogg
       |-Voices-pico.ogg
   |-images
     |-storymenu
       |-titles
         |-myweek.png
   |-_polymod_meta.json
```

Your custom week's JSON file will look something like the following:

```json
{
  "version": "1.0.0",
  "name": "MY CUSTOM WEEK",
  "titleAsset": "storymenu/titles/myweek",
  "background": "#F9CF51",
  "songs": ["mychart"],
  "visible": true,
  "props": [
    {
      "assetPath": "storymenu/props/dad",
      "scale": 1.0,
      "offsets": [100, 60],
      "animations": [
        {
          "name": "idle",
          "prefix": "idle0",
          "frameRate": 24
        }
      ]
    },
    {
      "assetPath": "storymenu/props/bf",
      "scale": 1.0,
      "offsets": [150, 80],
      "animations": [
        {
          "name": "idle",
          "prefix": "idle0",
          "frameRate": 24
        },
        {
          "name": "confirm",
          "prefix": "confirm0",
          "frameRate": 24
        }
      ]
    }
  ]
}
```

There's a lot of info here! Let's break it down:

- `version`: The version number for the Level data file format. Leave this at `1.0.0`.
- `name`: The readable name for the Level, as displayed at the top right of the Story Menu.
- `titleAsset`: The asset to use for the level name in the list of level, relative to the `images` folder in your mod folder.
- `background`: The background to use for the level. `#F9CF51` is the classic yellow, but this field takes either a color code OR an image file path (relative to the `images` folder in your mod folder).
- `songs`: A list of song IDs to include in the week.
- `visible`: Whether this story level is visible in the Story Menu.
- `props`: Data for the props to display on the Story Menu when the level is selected. For example, Week 1 will display Daddy Dearest, Boyfriend, and Girlfriend.

When the game starts, it queries the list of available levels by looking in the `data/levels` folder for JSON files, which it then uses to populate the Story Menu, and then the Freeplay Menu (in non-alphabetical views, songs in Freeplay appear in order by what level they are included in).

If you want your custom song to only show up in Freeplay, you can just create a custom week and set the `visible` property to false, and the songs will show up in Freeplay!
