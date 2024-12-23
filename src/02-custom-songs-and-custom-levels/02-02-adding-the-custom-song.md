# Adding The Custom Song

At the end of [Creating A Chart](02-01-creating-a-chart.md) we learned that `.fnfc` files were just `.zip` archives, so we can simply rename it and unzip it. Once we have thse files, we just need to put them in the correct spots in our mod folder!

- The `manifest.json` file can be discarded, our mod won't need it.
- The `metadata.json` and `chart.json` files need to go into the `data/songs/<songid>` folder, replacing `<songid>` with the internal name for our song.
- The OGG files need to go into `songs/<songid>`, again replacing `<songid>` with the internal name of our song.

We'll end up with something like this.

```
-mods
 |-myMod
   |-data
     |-songs
       |-mychart
         |-mychart-metadata.json
         |-mychart-chart.json
   |-songs
     |-mychart
       |-Inst.ogg
       |-Voices-bf.ogg
       |-Voices-pico.ogg
   |-_polymod_meta.json
```

When the game starts, it queries the list of available songs by looking in the `data/songs` folder for `<songid>/<songid>-metadata.json` files, which it then uses to find the chart file and the requisite song files. Neat! But right now, if you boot up the game, this doesn't do anything. You'll see it mentioned in the logs with no complaints, but it's not playable in Story Mode or Freeplay, what gives?

```
source/funkin/play/song/Song.hx:579: Fetching song metadata for mychart
source/funkin/data/song/SongRegistry.hx:103:   Loaded entry data: Song(mychart)
```

The fix is simple; every song must be part of a Story Mode level to appear in Freeplay.