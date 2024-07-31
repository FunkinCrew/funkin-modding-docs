# Mod Load Order

You may wonder what happens in the case where multiple mods provide a given file.

The answer is simple; mod order matters. If you have two mods installed which replace a particular asset, the mod which loads last will get precedence over mods that get loaded earlier, similar to Minecraft's resource pack system. This is evaluated on a per-file basis, so if Mod A replaces Pico and GF and Mod B replaces only GF, and Mod B is loaded after Mod A, you'll see the Pico from Mod A and the Girlfriend from Mod B.

In the current version of Friday Night Funkin', there is no accessible means of altering mod load order. Mods will load in alphabetical order by default, with dependencies being loaded first.