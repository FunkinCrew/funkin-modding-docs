# Creating a Chart

To create a chart, access the Chart Editor tool. This can be found in-game by accessing the Debug menu from the main menu (this is bound to `~` by default). You can also access it by adding a keybind for "Debug Chart" in the options menu (not bound by default), then pressing the bound key while playing a song.

From here, you can create a new chart from audio files, import one from an older version of the game, or build a chart from existing in-game chart data.

Detailed use of the chart editor deserves its own guide, but the basic should be fairly intuitive. For now, let's assume you've made a chart of your favorite song, and want to turn it into a mod people can play.

## Dissecting Your FNFC File

When you save your chart, the game packages it up into a `.fnfc` file, which makes it easy to share with other charters and collaborate. It includes the audio for the song, along with the note data and some metadata files to go with it.

To add the song to our mod, we need to get that info out. This is fairly easy, because an FNFC file is actually secretly a ZIP file! Rename your `mychart.fnfc` to `mychart.zip`, replacing the file extension so that your operating system recognizes it as a ZIP, and extract it to reveal its contents, which will be something like:

```
-manifest.json
-mychart-metadata.json
-mychart-chart.json
-Inst.ogg
-Voices-bf.ogg
-Voices-pico.ogg
```
