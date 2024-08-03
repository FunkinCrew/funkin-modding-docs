# Scripted Classes

Funkin's implementation of HScript uses a system of scripted classes. To create a scripted class, create an `.hxc` file in your `mods/mymod/scripts/` folder, and, using Haxe syntax, create a new class which extends the base class for the type of object you are scripting, like so:

```haxe
// Remember to import each class you want to reference in your script!
import funkin.play.song.Song;

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

## List of Scriptable Classes

There is a predefined list of classes which the game has set up to be scriptable, and will automatically load and execute when relevant. More of these will be added in the future.

- `funkin.play.song.Song` for providing unique behavior to custom songs, including playing cutscenes and other stuff
- `funkin.play.character.BaseCharacter` for providing unique behavior to custom characters (such as playing custom animations in certain circumstances)
- `funkin.play.stage.Stage` for providing unique behavior to custom stages (such as creating custom moving props and defining when props animate or when sound effects play in sync with the stage)
- `funkin.ui.story.Level` for providing unique behavior to levels in Story Mode
- [UPCOMING IN 0.5.0] `funkin.play.notes.notekind.NoteKind` for providing unique visuals and behavior to certain kinds of notes (which can then be placed in the Chart Editor!)
- `funkin.play.event.SongEvent` for creating custom Song Events (which you can place in the Chart Editor!)
- `funkin.play.notes.notestyle.NoteStyle` for modifying the behavior of custom note styles.
- `funkin.play.cutscene.dialogue.Conversation` for providing unique behavior to custom dialogue conversations
- `funkin.play.cutscene.dialogue.DialogueBox` for providing unique behavior to custom dialogue boxes used in conversations
- `funkin.play.cutscene.dialogue.Speaker` for providing unique behavior to custom speakers used in conversations
- `funkin.ui.freeplay.Album` for defining custom behavior for Freeplay Albums.
- `funkin.modding.module.Module` for custom scripted Modules, which are scripts which receive events everywhere, rather than only in a specific context.

There are also scripted classes are also set up to be scriptable, but will only be useful if they're accessed from another script. Expect more of these to be added in the future.

- `funkin.graphics.FunkinSprite` for basic static or animated sprites.
- `funkin.ui.MusicBeatState` for groups of sprites associated with a camera, which represents a given game state
- `funkin.ui.MusicBeatSubState` for groups of sprites representing a substate of an existing state
- `funkin.play.stage.Bopper` for sprites which will play an idle animation to the beat of the music when they are part of a Stage.
- `funkin.graphics.adobeanimate.FlxAtlasSprite` for generic sprites which use Adobe Animate texture atlases
- `flixel.addons.display.FlxRuntimeShader` for custom GLSL shaders
- `flixel.group.FlxSpriteGroup` for groups of sprites which are included inside a State and manipulated together
- `flixel.FlxSprite`
- `flixel.FlxState`
- `flixel.FlxSubState`
- `flixel.addons.transition.FlxTransitionableState`
- `flixel.addons.ui.FlxUIState`
