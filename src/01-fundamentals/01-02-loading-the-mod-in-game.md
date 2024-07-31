# Loading the Mod In-Game

Now that you have a metadata file, you can start the game! Pro tip, if you run the game from the command line, you can see lots of useful debug messages, like these messages that indicate your mod has loaded!

```shell
source/funkin/modding/PolymodHandler.hx:316: Found 5 mods when scanning.
source/funkin/modding/PolymodHandler.hx:118: Attempting to load 5 mods...
...
source/funkin/modding/PolymodErrorHandler.hx:79: [INFO-] LOADING MOD - Preparing to load mod ../../../../example_mods/introMod
source/funkin/modding/PolymodErrorHandler.hx:79: [INFO-] LOADING MOD - Done loading mod ../../../../example_mods/introMod
...
source/funkin/modding/PolymodHandler.hx:169: Mod loading complete. We loaded 5 / 5 mods.
```

Neat! But right now, your mod doesn't do anything.
