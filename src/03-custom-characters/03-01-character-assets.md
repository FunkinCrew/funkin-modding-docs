# Character Spritesheet Formats

The individual sprites of a character's animations must be combined into a spritesheet for the game to use them. Friday Night Funkin' supports one of several formats:

- `sparrow`: Combines the images into a large sheet, then provides an XML file containing the coordinates of each frame with it. Can be exported directly from Adobe Animate or Flash CS6 using the `Generate Sprite Sheet` option, or can be created from individual frames using [Free Texture Packer](http://free-tex-packer.com/) (note that Free Texture Packer refers to this format as Starling).

- `packer`: Combines images into a sheet, then provides a TXT file containing the coordinates of each frame.

- `animateatlas`: Created exclusively when using Adobe Animate, this exports individual symbols into a large sheet, then provides a JSON file with data to split up each symbol, then provides a second JSON to arrange those symbols into animations. Great for performance, especially for characters which were made by rearranging smaller parts. We use the [FlxAnimate](https://github.com/Dot-Stuff/flxanimate) Haxelib for this.

- `multisparrow`: Allows for different groups of animations to be exported into separate Sparrow spritesheets, then combined together into one character.
