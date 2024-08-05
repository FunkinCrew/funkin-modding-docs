# Fixing Character Offsets

Uh Oh! Upon using your character in a song, you might have noticed that with each note hit, the character has weird offsets which makes it wobble back and forth. Let's fix that.

## Accessing the Animation Editor

To fix offsets for you character, you first have to access the Animation Editor tool. This can be found in-game by accessing the Debug menu from the main menu (this is bound to `~` by default) and selecting "Animation Editor" option.

Once you have accessed the tool, it might be a little overwhelming at first, but everything is pretty straightforward.

## Fixing the Offsets

The first thing you have to do is click `2` on your keyboard to switch to `Animation Mode` in order to properly fix offsets for each animation. Then, you need to select your character from the `Character` section in the UI box that is located in the top-left corner.

*HINT:* The best thing to do to speed up your process, it to toggle `Onion Skin` mode by pressing `F`. This will show the previous animation played being half transparent. This can help speeding up the proccess, since you will be able to to properly line up the animation with the previous one.

The UI will show you all of the possible controls and shortcuts, to make your proccess of fixing the character offsets much easier.

## Saving Offsets

Once you are happy with your result, simply press `ESC` on your keyboard to save the `Character Data` file.
  - Currently there is a bug which makes the file saving system not automatically put character's ID in the file name, which you will have to do yourself. Simply name the file the ID of your character followed by `.json`.

From the ["Creating a Character"](03-02-creating-a-character.md) chapter you will know, that you have to place this character data JSON file in `data/characters`. Then, you can simply use [Hot Reloading](../01-fundamentals/01-05-hot-reloading.md) to check the offsets without restarting the game.