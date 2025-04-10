# The Metadata File

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
  "api_version": "0.6.3",
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
- `api_version`: A version number used to determine if mods are compatible with your copy of Funkin'. Change this to the version number for Friday Night Funkin' that you want to support, preferably the latest one (`0.6.3` at time of writing.).
- `mod_version`: A version number specifically for your mod. Choose any version or leave it at `1.0.0`.
- `license`: The license your mod is distributed under. [Pick one from here](https://opensource.org/licenses) or just leave it as `Apache-2.0`.

A Contributor has the following fields:

- `name`: The contributor's name.
- `role`: *(optional)* The role the contributor played, for example "Artist" or "Programmer"
- `email`: *(optional)* A contact email
- `url`: *(optional)* A homepage URL

Many of these fields are intended to be used in the future by an upcoming Mod Menu interface, which will allow users to organize their mods.