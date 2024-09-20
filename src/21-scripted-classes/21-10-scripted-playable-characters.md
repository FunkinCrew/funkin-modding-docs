# Creating a Friday Night Funkin' Mod - Scripted Playable Characters

This chapter will walk you through the process of adding a script to a Playable Character, and giving examples of the kind of custom behavior which can be implemented with this functionality.

Start by creating a scripted class file with the `.hxc` extension (in the `mods/mymod/scripts/characters` if you want to keep things organized).

```haxe
// Remember to import each class you want to reference in your script!
import funkin.play.character.SparrowCharacter;

// Choose a name for your scripted class that will be unique, and make sure to specifically extend the correct character class.
// SparrowCharacter is the one to use for XML-based characters.
// This class's functions will override the default behavior for the character.
class WhittyCharacter extends SparrowCharacter {
	public function new() {
        // The constructor gets called whenever the character is spawned.
        // The constructor takes one parameter, which is the song ID for the song you are applying the script to.
		super('whitty');
	}

    // Add override functions here!
}
```

You can then add override functions to perform custom behavior.

## Custom Unlock Behavior

The most important thing to override here is the `isUnlocked` function, which lets you define whether the player can access the given character in Freeplay.

```haxe
  // An example of overriding the `isUnlocked` function.
  // This is the logic for Pico, which requires checking the completion status of a given story week.
  // You can put any logic you want here.
  override function isUnlocked():Bool {
    return Save.instance.hasBeatenLevel('weekend1');
  }
```
