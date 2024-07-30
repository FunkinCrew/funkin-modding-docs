# Creating a Friday Night Funkin' Mod - Fundamentals

This guide will walk you through the process of creating a functioning, fully compatible Friday Night Funkin' mod, using the game's official systems for loading custom content and scripts. Once your mod is complete, you will be able to place it in the `mods` folder in your game install and use its content in-game without overriding the base game content and still maintain compatibility with other mods.

This entry in particular goes through a lot of core concepts of modding in Funkin' that will get used in other guides, so be sure to read through it carefully.

## The Metadata File

To start, create a new folder within your `mods` folder. This is where your mod's assets and scripts will live. Next, create a new text file, and change its name to `_polymod_meta.json`. Make sure you didn't accidentally name it `_polymod_meta.json.txt`!

Inside this file, we will put the information the game needs in order to learn about your mod. I recommend doing this with a program like [Visual Studio Code](https://code.visualstudio.com/), it will correct you if you accidentally misplace a comma or something.

```json
{
  "title": "Intro Mod",
  "description": "An introductory mod.",
  "contributors": [
    {
      "name": "EliteMasterEric"
    }
  ],
  "dependencies": {
    "modA": "1.0.0"
  },
  "optionalDependencies": {
    "modB": "1.3.2"
  },
  "api_version": "0.1.0",
  "mod_version": "1.0.0",
  "license": "Apache-2.0"
}
```

`_polymod_meta.json` has the following fields:

- `title`: A readable name for the mod.
- `description`: A readable description for the mod.
- `contributors`: A list of Contributor objects.
- `homepage`: A URL where users can learn more about your mod.
- `dependencies`: A map of mod IDs which are mandatory dependencies, along with their version numbers.
  - These are the mods which must also be loaded in order for this mod to load.
  - If the mod is not included, it will fail.
  - The mod list will be reordered such that dependencies load first.
- `optionalDependencies`: A map of mod IDs which are optional dependencies, along with their version numbers.
  - These mods do not necessarily need to be installed for this mod to load, but they will still force the mod list to be reordered so that the dependencies load before this mod.
- `api_version`: A version number used to determine if mods are compatible with your copy of Funkin'. Leave this as `0.1.0`.
- `mod_version`: A version number specifically for your mod. Choose any version or leave it at `1.0.0`.
- `license`: The license your mod is distributed under. [Pick one from here](https://opensource.org/licenses) or just leave it as `Apache-2.0`.

A Contributor has the following fields:

- `name`: The contributor's name.
- `role`: *(optional)* The role the contributor played, for example "Artist" or "Programmer"
- `email`: *(optional)* A contact email
- `url`: *(optional)* A homepage URL

Many of these fields are intended to be used in the future by an upcoming Mod Menu interface, which will allow users to organize their mods.

## Loading the Mod In-Game

Now that you have a metadata file, you can start the game! Pro tip, if you run the game from the command line, you can see lots of useful debug messages, like these messages that indicate your mod has loaded!

```
source/funkin/modding/PolymodHandler.hx:316: Found 5 mods when scanning.
source/funkin/modding/PolymodHandler.hx:118: Attempting to load 5 mods...
...
source/funkin/modding/PolymodErrorHandler.hx:79: [INFO-] LOADING MOD - Preparing to load mod ../../../../example_mods/introMod
source/funkin/modding/PolymodErrorHandler.hx:79: [INFO-] LOADING MOD - Done loading mod ../../../../example_mods/introMod
...
source/funkin/modding/PolymodHandler.hx:169: Mod loading complete. We loaded 5 / 5 mods.
```

Neat! But right now, your mod doesn't do anything.

## Asset Replacement

The key thing that Polymod allows you to do is to replace assets. This is done by adding those files to your mods folder in the same location as they would go.

For example, you can replace Girlfriend's sprites by placing your new sprites in the same location as they are in the `assets` folder, which would be `shared/images/characters/GF_assets.png`.

In other words, structure your mod like so:

```
-assets
-manifest
-plugins
-mods
 |-myMod
   |-shared
     |-images
       |-characters
         |-GF_assets.png
         |-GF_assets.xml
   |-_polymod_metadata.json
-Funkin.exe
```

When the game goes to load a character's sprites, it will make a request internally to retrieve the `assets/shared/images/characters/GF_assets.png` file to use for the texture (and the corresponding `XML` to split the image into individual frames). When it does, Polymod intercepts that request and checks if there is a file of that name among the loaded mods, and if so, it will use that instead.

## Asset Additions

Polymod also allows you to add new files to the game. This is notable, as trying to place new files into the `assets` directory doesn't work, the game won't recognize those files.

The game still needs to get told to load those assets for them to get used, but there are many functions which load all the files in a given folder (such as the Song Registry, the Character Registry, the Stage Registry, etc). We'll look more into those later.

## Mod Load Order

You may wonder what happens in the case where multiple mods provide a given file.

The answer is simple; mod order matters. If you have two mods installed which replace a particular asset, the mod which loads last will get precedence over mods that get loaded earlier, similar to Minecraft's resource pack system. This is evaluated on a per-file basis, so if Mod A replaces Pico and GF and Mod B replaces only GF, and Mod B is loaded after Mod A, you'll see the Pico from Mod A and the Girlfriend from Mod B.

In the current version of Friday Night Funkin', there is no accessible means of altering mod load order. Mods will load in alphabetical order by default, with dependencies being loaded first.

## Conclusion

This guide has covered the fundamentals of creating mods for Friday Night Funkin'. In other sections, we will go over how to add different types of custom content.
