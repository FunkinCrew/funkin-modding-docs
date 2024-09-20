# Creating a Friday Night Funkin' Mod - Scripted Characters

This chapter will walk you through the process of adding a script to a Character, and giving examples of the kind of custom behavior which can be implemented with this functionality.

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

## Character Classes

If you use a different animation type for a character, you need to specify a different base script class, otherwise the character will fail to load.

- `funkin.play.character.SparrowCharacter` is used for characters that have Sparrow spritesheet animations.
- `funkin.play.character.MultiSparrowCharacter` is used for characters that have several Sparrow spritesheet animations to combine into one character.
- `funkin.play.character.PackerCharacter` is used for characters that have Packer spritesheet animations.
- `funkin.play.character.AnimateAtlasCharacter` is used for characters that have Adobe Animate texture atlases.
- `funkin.play.character.BaseCharacter` has empty stubs for all the rendering and animation handlers, and is only useful for people who want to reimplement their character's animation system by hand.