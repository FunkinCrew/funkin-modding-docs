# Modifying an Existing Sticker Pack

You can use the [JSONPatch](../10-appending-and-merging-files/10-02-merging-files.md) feature to add or remove stickers from an existing sticker pack.

For example, to add to Boyfriend's standard sticker pack, you can use the following JSON Patch file (placed in `mods/mymod/_merge/data/stickerpacks/standard-bf.json`, use a different file path to patch a different sticker pack):

```jsonc
[
    // Add an asset path to the end of the sticker list.
    { "op": "add", "path": "/stickers/-", "value": "path/to/custom/sticker" }
]
```
