# Asset Replacement and Additons

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
   |-_polymod_meta.json
-Funkin.exe
```

When the game goes to load a character's sprites, it will make a request internally to retrieve the `assets/shared/images/characters/GF_assets.png` file to use for the texture (and the corresponding `XML` to split the image into individual frames). When it does, Polymod intercepts that request and checks if there is a file of that name among the loaded mods, and if so, it will use that instead.

## Asset Additions

Polymod also allows you to add new files to the game. This is notable, as trying to place new files into the `assets` directory doesn't work, the game won't recognize those files.

The game still needs to get told to load those assets for them to get used, but there are many functions which load all the files in a given folder (such as the Song Registry, the Character Registry, the Stage Registry, etc). We'll look more into those later.