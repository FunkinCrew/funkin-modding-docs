# Adding Variations to Existing Songs

Through modding, it is possible to add new variations to existing songs. This is great for adding a new difficulty or remix to an existing song (even if that song is from another mod).

## Obtaining Required Files

The first step is to compose a new remix for the song. If you're making a playable character remix, the composer will have to manually make sure the original vocals line up if you want the option to use alternate instrumentals.

You then have to chart this remix. When you're done, you should have an `Inst.ogg` file, two `Voices` OGG files, a `metadata.json` and a `chart.json`.

## Placing the Files

Next, place the assets in the correct spots in our mod folder! Rename each of the files, adding a variation ID of your choice to the end (so if you're making an erect remixes, rename `Inst.ogg` to `Inst-erect.ogg`):

```
-mods
 |-myMod
   |-data
     |-songs
       |-mychart
         |-mychart-metadata-erect.json
         |-mychart-chart-erect.json
   |-songs
     |-mychart
       |-Inst-erect.ogg
       |-Voices-bf-erect.ogg
       |-Voices-pico-erect.ogg
   |-_polymod_meta.json
```

## Registering the Variation in the JSON Data

Each chart includes a `songVariations` array, which lets the game know which variations the song has available so it can query their respective metadata files. In order to get the game to load your custom variation, you need to modify the `metadata.json` file for the song's chart, so the game knows that variation exists.

### If the song is from your own mod

If the base song you're adding the remix to is from your own mod, you can just add the variation to the `metadata.json` for your chart.

Add your variation ID to the `playData.songVariations` array (creating the key if it doesn't exist).

```json
{
    "playData": {
        "songVariations": ["erect"] // Add your new variation to this array.
        // ...
    }
    // ...
}
```

### If the song is from the base game, or a different mod

If the base song you're adding to is from a different mod, you don't want to replace the underlying data in case it changes. You want to instead apply a JSON Patch to the file (which Polymod provides the ability to do).

Create a `_merge` folder in your mod folder, then create a file within that directory whose path matches the one you want to patch, like so:

```
-mods
 |-myMod
   |-_merge
     |-data
       |-songs
         |-mychart
           |-mychart-metadata.json
```

Then we apply a simple patch, which adds a new value to the `playData.songVariations` array. Edit the JSON file and add these contents:

```json
[
    { "op": "add", "path": "/playData/songVariations/-", "value": "erect" } // Add a new value erect to the end of the songVariations array.
]
```

The patching system is very flexible; it works on any JSON file (base game or provided by another mod) and has support for advanced behavior. See [Merging Files](../10-appending-and-merging-files/10-02-merging-files.md) for more information.

## Conclusion

Now, when you start the game, your additional variation should be available in-game!

If you created a character remix, make sure the player character for the remix is included in the `ownedCharacters` data for your custom playable character. See [Custom Playable Characters](../05-custom-playable-characters/05-00-custom-playable-characters.md) for more info.
