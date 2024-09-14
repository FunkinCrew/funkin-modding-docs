# What Are Variations?

Variations are groups of difficulties for a given song which share metadata.

As an example, the song DadBattle has eight separate difficulties (at time of writing). These are Easy, Normal, Hard, Erect (Erect Mix), Nightmare (Erect Mix), Easy (Pico Mix), Normal (Pico Mix), and Hard (Pico Mix).

These are divided into three variations; Default, Erect, and Pico. Each variation defines information like BPM (and BPM changes), artist, charter, which album the song is from, which stage to use, which character to use in those stages, and which instrumental and vocal track to use. The variation then defines which difficulties it includes, and the chart data for that variation specifies the events for that variation, and the note data and scroll speed for each difficulty.

This means that, in order to make one of these values different for a specific difficulty or remix (including changing the events), you must put that difficulty into a new variation.

The `metadata.json` file for a song defines what variations exist for that song; the game then looks for `metadata-<variationID>.json` and `chart-<variationID>.json` files for each listed variation.
