# Creating a Friday Night Funkin' Mod - Scripted Songs

This guide will walk you through the process of creating a functioning, fully compatible Friday Night Funkin' mod, using the game's official systems for loading custom content and scripts. Once your mod is complete, you will be able to place it in the `mods` folder in your game install and use its content in-game without overriding the base game content and still maintain compatibility with other mods.

This chapter will walk you through the process of adding a script to a Song, and giving examples of the kind of custom behavior which can be implemented with this functionality.

Start by creating a scripted class file with the `.hxc` extension (in the `mods/mymod/scripts/songs` if you want to keep things organized).

```haxe
// Remember to import each class you want to reference in your script!
import funkin.play.song.Song;

// Choose a name for your scripted class that will be unique, and make sure to specifically extend the Song class.
// This class's functions will override the default behavior for the song.
class BallisticSong extends Song {
	public function new() {
        // The constructor gets called once, when the game loads.
        // The constructor takes one parameter, which is the song ID for the song you are applying the script to.
		super('ballistic');
	}

    // Add override functions here!
}
```

You can then add override functions to perform custom behavior. Here are some useful snippets:

