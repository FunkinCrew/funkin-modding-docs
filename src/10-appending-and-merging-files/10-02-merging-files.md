# Merging

Merging files into a data file is required for more complicated operations, such as inserting data somewhere other than the start of the document, replacing certain data with new data, or even deleting certain data from the document.

By using `_merge` files, rather than replacing the data files entirely, you make your mod fully compatible with both changes to the base game and to changes made by other mods. Merge files are applied in mod load order, meaning that multiple mods can make changes to the same file without any conflicts!

### Merging into TXT Files
**TODO**

### Merging into CSV/TSV Files

CSV and TSV files can be merged as well. In this case, the mod loader will look for any rows in the base file whose first cell matches the same value as those in the merge file, and replace them with the rows from the merge file.

### Merging into XML Files

*NOTE: The behavior of Merging XML files may change significantly in the near future.*

For XML, you must create an XML document containing the desired, values, with additional information to inform Polymod about where to insert it.

Say you have a big complicated XML file at `data/stuff.xml` with lots of nodes:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<data>
   <!--lots of complicated stuff-->
   <mode id="difficulty" values="easy"/>
   <!--even more complicated stuff-->
</data>
```

And you want it to say this instead:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<data>
   <!--lots of complicated stuff-->
   <mode id="difficulty" values="super_hard"/>
   <!--even more complicated stuff-->
</data>
```

Basically we want to change this one tag from this:

```xml
<mode id="difficulty" values="easy"/>
```

to this:
```xml
<mode id="difficulty" values="super_hard"/>
```

This is the file you would put in `<modroot>/<mergeFolder>/data/stuff.xml`:
```xml
<?xml version="1.0" encoding="utf-8" ?>
<data>
    <mode id="difficulty" values="super_hard">
        <merge key="id" value="difficulty"/>
    </mode>
</data>
```

This file contains both data and merge instructions. The `<merge>` child tag tells the mod loader what to do, and will not be included in the final data. The actual payload is just this:

```xml
<mode id="difficulty" values="super_hard">
```

The `<merge>` tag instructs the mod loader thus:

* Look for any tags with the same name as my parent (in this case, `<mode>`)
* Look within said tags for a `key` attribute (in this case, one named `"id"`)
* Check if the key's value matches what I'm looking for (in this case, `"difficulty"`)

As soon as it finds the first match, it stops and merges the payload with the specified tag. Any attributes will be added to the base tag (overwriting any existing attributes with the same name, which in this case changes values from "easy" to just "super_hard", which is what we want). Furthermore, if the payload has child nodes, all of its children will be merged with the target tag as well.

### Merging into JSON Files

Merging into JSON files is done using a [JSON Patch](https://jsonpatch.com/) document. (NOTE: This significantly differs from JSON patch files created for v0.4.1 and earlier, which used a different system that honestly kinda sucked).

Say we have a JSON data file `data/songs/mysong-metadata.json` like below:

```json
{
  "version": "2.1.0",
  "playData": {
    "characters": {
      "player": "bf",
      "opponent": "dad"
    },
    "difficulties": [
      "easy", "normal", "hard"
    ],
    "garbageValue": 37,
    "stage": "mainStage"
  }
}
```

We can modify the above data with a document `mods/mymod/_merge/data/songs/mysong-metadata.json`:

```jsonc
[
  { "op": "replace", "path": "/playData/characters/opponent", "value": "monster" }, // Replace the value of opponent with monster.
  { "op": "add", "path": "/playData/characters/girlfriend", "value": "nene" }, // Add a new key girlfriend with the value Nene.
  { "op": "add", "path": "/playData/difficulties/1", "value": "funky" }, // Add a new value funky to the difficulty array, after easy
  { "op": "add", "path": "/playData/difficulties/-", "value": "expert" }, // Add a new value expert to the end of the difficulty array.
  { "op": "remove", "path": "/playData/garbageValue" }, // Remove the key garbageValue from the data entirely
  { "op": "test", "path": "/playData/garbageValue", "value": 37 } // Test that a given value is in the JSON. If this operation fails, the patches will be rejected.
]
```

The `op`erations supported are `add`, `remove`, `replace`, `move`, `copy`, and `test`. If any operation in a JSON Patch document fails, all of the modifications in that file will be reverted.

The `add`, `replace`, and `test` operations require a `value` key (which can be any JSON data, including an array or object), and the `move` and `copy` operations require a `from` key, which is a path value indicating where to move or copy from.

The `path` must be a string of either property names or array indexes (starting at 0), starting with and separated by slashes (`/`). For example, `/playData/characters/opponent`.

The `path` may also be a JSONPath string, which allows robustly specifying a target path with support for filtering logic. You can read more here: https://goessner.net/articles/JsonPath/
