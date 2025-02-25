# Scripted Classes

Funkin's implementation of HScript uses a system of scripted classes. To create a scripted class, create an `.hxc` file in your `mods/mymod/scripts/` folder, and, using Haxe syntax, create a new class which extends the base class for the type of object you are scripting, like so:

```haxe
// Package your scripts to help avoid conflicts with other mods!
package mymod.mysubpackage;

// Remember to import each class you want to reference in your script!
import funkin.play.song.Song; // or use ScriptedSong, it doesn't matter

// Choose a name for your scripted class that will be unique
// Also specify the class you are extending, we choose Song here.
// This script's behaviors will extend the default behavior of the song.
class BallisticSong extends Song {
	public function new() {
        // You have to call the super constructor for the class you are extending, which may have different parameters.
        // Check the specific documentation for more info.
		super('ballistic');
	}
}
```

## File Structure and Packages

A `.hxc` script file will run if and only if it's placed somewhere within the `scripts` folder of your mod root. To avoid conflicts with other mods, it's recommended to do 2 things:

You should try to "package" all your scripts. For example, if you have a script `mymod/scripts/mymod/mysubpackage/MyScript.hxc`, you should have the first line of your script be:

```haxe
package mymod.mysubpackage;
```

This creates a unique namespace for your script file so scripts from other mods don't override any classes in it. Also note that by doing this, you will also need to include the package name when initializing a script class instance, like:

```haxe
var someVar:ScriptedFunkinSprite = ScriptedFunkinSprite.init("mymod.mysubpackage.MyScript");
```

Also, try to also structure your script folders like you would for the source code a typical Haxe project. Script files are also kinda treated like mod assets, so if multiple mods have the same script filename at the same relative path, one is going to end up overriding the others. The folder structure should follow the same as your package structure, with some name unique to your mod at top-level. Though not *technically* necessary, it's good practice for stability and compatibility with other mods.

## List of Scriptable Classes

There is a predefined list of classes which the game has set up to be scriptable, and will automatically load and execute when relevant. More of these will be added in the future.

- `funkin.play.song.Song` for providing unique behavior to custom songs, including playing cutscenes and other stuff. See [Scripted Songs](21-scripted-classes/21-01-scripted-songs.md).
	- See also [Video Cutscenes](21-scripted-classes/21-03-video-cutscenes.md), [Ingame Cutscenes](21-scripted-classes/21-04-ingame-cutscenes.md), and [Dialogue Cutscenes](21-scripted-classes/21-05-dialogue-cutscenes.md)
- `funkin.play.character.BaseCharacter` for providing unique behavior to custom characters (such as playing custom animations in certain circumstances). See [Scripted Characters](21-scripted-classes/21-05-scripted-characters.md).
	- Note that you need to choose the correct subclass of this class for the animation type of your character!
	- `funkin.play.character.SparrowCharacter` is used for characters that have Sparrow spritesheet animations.
	- `funkin.play.character.MultiSparrowCharacter` is used for characters that have several Sparrow spritesheet animations to combine into one character.
	- `funkin.play.character.PackerCharacter` is used for characters that have Packer spritesheet animations.
	- `funkin.play.character.AnimateAtlasCharacter` is used for characters that have Adobe Animate texture atlases.
	- `funkin.play.character.BaseCharacter` has empty stubs for all the rendering and animation handlers, and is only useful for people who want to reimplement their character's animation system by hand.
- `funkin.play.stage.Stage` for providing unique behavior to custom stages, such as creating custom moving props and defining when props animate or when sound effects play in sync with the stage. See [Scripted Stages](21-scripted-classes/24-06-scripted-stages.md).
- `funkin.ui.story.Level` for providing unique behavior to levels in Story Mode. See [Scripted Story Levels](21-scripted-classes/25-07-scripted-story-levels.md).
- `funkin.play.notes.notekind.NoteKind` for providing unique visuals and behavior to certain kinds of notes, which can then be placed in the Chart Editor. See [Custom Note Kinds](21-scripted-classes/26-00-custom-note-kinds.md).
- `funkin.play.event.SongEvent` for creating custom Song Events, which you can place in the Chart Editor and which perform game actions when they are reached. See [Custom Song Events](21-scripted-classes/28-00-custom-note-kinds.md)
- `funkin.ui.freeplay.charselect.PlayableCharacter` for providing unique behavior to custom playable characters. See [Scripted Playable Characters](21-scripted-classes/25-10-scripted-playable-characters.md)
- `funkin.ui.freeplay.FreeplayStyle` for defining the sprites and colors used by the Freeplay menu when a given character is selected. See [WIP]
- `funkin.play.notes.notestyle.NoteStyle` for modifying the behavior of custom note styles. See [WIP]
- `funkin.play.cutscene.dialogue.Conversation` for providing unique behavior to custom dialogue conversations. See [Dialogue Cutscenes](21-scripted-classes/21-05-dialogue-cutscenes.md)
- `funkin.play.cutscene.dialogue.DialogueBox` for providing unique behavior to custom dialogue boxes used in conversations. See [Dialogue Cutscenes](21-scripted-classes/21-05-dialogue-cutscenes.md)
- `funkin.play.cutscene.dialogue.Speaker` for providing unique behavior to custom speakers used in conversations. See [Dialogue Cutscenes](21-scripted-classes/21-05-dialogue-cutscenes.md)
- `funkin.ui.freeplay.Album` for defining custom behavior for Freeplay Albums. See [WIP]

There is also `funkin.modding.module.Module` for custom scripted Modules, which are singleton script classes which receive events everywhere, rather than only in a specific context. See [Scripted Modules](30-scripted-modules/30-00-scripted-modules.md) for more information on how these work.

There are also scripted classes are also set up to be scriptable, but will only be useful if they're accessed from another script. Expect more of these to be added in the future.

- `funkin.graphics.FunkinSprite` for basic static or animated sprites.
- `funkin.graphics.adobeanimate.FlxAtlasSprite` for generic sprites which use Adobe Animate texture atlases
- `flixel.group.FlxSpriteGroup` for groups of sprites which are included inside a state and manipulated together
- `funkin.ui.MusicBeatState` for groups of sprites which represents a given game state. Includes additional utilities for handling script events.
- `funkin.ui.MusicBeatSubState` for groups of sprites representing a substate of an existing state
- `flixel.addons.display.FlxRuntimeShader` for custom GLSL shaders
- `funkin.play.stage.Bopper` for sprites which will play an idle animation to the beat of the music when they are part of a Stage.
- `flixel.FlxSprite` for basic static or animated sprites. Use this only if you can't use FunkinSprite.
- `flixel.FlxState` for basic groups of sprites which represent a given game state. Use this only if you can't use MusicBeatState.
- `flixel.FlxSubState` for groups of sprites representing a substate of an existing state
