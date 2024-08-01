# What is HScript?

HScript is an interpreted scripting language used by Polymod to provide custom functionality to Friday Night Funkin'. The game detects scripts provided in `.hxc` files, interprets them, and executes them to perform custom functionality in-game.

Mods are not the only thing that utilizes this functionality; the base game itself uses scripts to play animations and cutscenes, manipulate stage props, and even add custom gameplay, in a manner that allows for faster iteration than would be possible without scripts.

HScript is extremely similar to Haxe, and provides access to almost all the variables and classes available in the game, with a few notes:

- Each scripted class must have a unique name from every other scripted class. If your mod has two scripted classes with the same name, or even if two different mods have scripted classes of the same name, one copy will be completely suppressed, which can result in unexpected behavior.
- Private variables are simply accessible, be careful what you mess with.
- Certain classes are blacklisted, to help protect users against malicious scripts.
- `abstract enum`s (a Haxe language feature which provides values which act like an Enum, but are actually some other type like a String or Integer) are inaccessible. Check the code for the `abstract enum` you want to use and find the ACTUAL underlying value, and use that instead.
- `abstract`s (a Haxe language feature which applies additional methods to an existing class) are inaccessible. You will have to find some workaround to interact with these values.