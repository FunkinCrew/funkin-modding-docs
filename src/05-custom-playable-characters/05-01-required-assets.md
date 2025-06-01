# Required Assets

In order to make a fleshed out custom character that can be used from Character Select in Friday Night Funkin', you need a large number of textures, animations, and audio tracks:

- A [custom character](../03-custom-characters/03-00-custom-characters.md)
    - This requires a set of singing animations for the character.
- At least one custom song that uses that character; this can be either [a new song](../02-custom-songs-and-custom-levels/02-02-adding-the-custom-song.md) or a [variation added to an existing song](../02-custom-songs-and-custom-levels/02-05-adding-variations-to-existing-songs.md).
    - This requires an instrumental and split vocal tracks.
- A pixel icon asset to use for that character's icon in the Character Select grid.
    - This supports either a static image or a Sparrow spritesheet (which includes the animation to play when the character is selected).
- A namecard asset to use for that character's name above them in the Character Select menu.
    - The pixellation effect is done in code so this just needs to be a single static image.
- Animations for the character to use in the Character Select menu.
    - This is currently hard-coded to use an Adobe Animate texture atlas and cannot use a Sparrow spritesheet.
    - The character needs animations for unlock, idle, slide in, slide out, select, and deselect.
- Assets to use for the character's Girlfriend character to the left of them in the Character Select menu.
    - This is currently hard-coded to use an Adobe Animate texture atlas and cannot use a Sparrow spritesheet.
    - The character needs animations for unlock, idle, slide in, slide out, select, and deselect.
- Assets for the character to use on the Freeplay menu.
    - This is currently hardcoded to use an Adobe Animate texture atlas.
    - The character needs animations for leaping in, idle, confirm, and moving to character select. It also optionally has an idle and cartoon animation.
- Assets for the character's Freeplay skin and the backing card.
    - This requires a variety of assets but can use Boyfriend's as a fallback.
    - NOTE: This is currently hardcoded to BF or Pico.
- Assets for the character's animations in the Results screen.
    - Each rank has its own animation and music, but animations can be reused between ranks and results themes can fall back to the default.
    - Rank animations are Loss, Good, Great, Excellent, Perfect, and Perfect Gold (the base game uses the same animation for Perfect and Perfect Gold)
    - Each also can take its own music, but you can reuse Boyfriend's as a good placeholder.
