# Using a Custom Sticker Pack

There are two ways the game defines a given sticker pack to be used:

- Each [Playable Character](../05-custom-playable-characters/05-00-custom-playable-characters.md) defines the `stickerPack` variable, which specifies the sticker pack to be used by songs containing that character. For example, `bf` uses the `standard-bf` sticker pack. You can define a sticker pack to be used for your custom playable character by setting the `stickerPack` value, or modify which sticker pack is used by other playable characters by using [JSONPatch](../10-appending-and-merging-files/10-02-merging-files.md) to modify the `stickerPack` value of that character.
- Each song has a value in its metadata to define which sticker pack is used. Set the `playData.stickerPack` on a song (or use JSONPatch to modify metadata of an existing song) to override which sticker pack it uses.

The game checks and uses sticker packs in this order:

- The sticker pack chosen by the song.
- The sticker pack chosen by the playable character.
- The `default` sticker pack (which displays only Boyfriend). If you see only Boyfriend during a sticker transition, then you know neither the song or the playable character defines a sticker pack, and you should fix the issue.