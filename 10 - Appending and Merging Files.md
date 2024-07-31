# Appending and Merging Files

There will often be times where you want to modify the contents of an existing file. This is relatively straightforward for textures, but for data files, things get more complicated. You often don't want to replace the entire file, but instead just a smaller chunk, or even a single value. Thankfully, Polymod provides a function for doing this.

## Appending Files

Adding values to the end of a data file is pretty straight-forward, but it depends on the file type you want to append to.

Create a new file in the `_append` folder of your mod, with a path matching the file you want to append to. For example, to append to `assets/data/introText.txt`, you would place your file at `mods/mymod/_append/data/introText.txt`

### Appending to TXT Files

If the file extension of the append file is `.txt`, the contents of the file will be simply appended to the end of the target file.

### Appending to CSV/TSV Files

If the file extension of the append file is `.csv` or `.tsv`, the rows in the sheet will be added to the end of the target sheet.

### Appending to XML Files

TODO: Fill this out.

### Appending to JSON Files

If the file extension of the append file is `.json`, the value will be parsed and naively appended to the target data.

For example, given the source file `data/mydata.json`:

```json
{
  "test1": [1, 2, 3],
  "test2": {
    "foo": "bar"
  },
  "test3": "baz"
}
```

We can provide the file `mods/mymod/_append/data/mydata.json`:

```json
{
  "test4": "hello",
  "test2": {
    "fizz": "buzz"
  }
}
```

And Polymod will mutate it to get this result:

```jsonc
{
  // Unreferenced values are untouched.
  "test1": [1, 2, 3],
  // Included values are placed in directly, not merged!
  "test2": {
    "fizz": "buzz"
  },
  "test3": "baz",
  // New values are simply included.
  "test4": "hello"
}
```

If you want something more particular, see [Merging into JSON Files](#merging-into-json-files) for a more powerful and flexible approach.

## Merging

Merging files into a data file is required for more complicated operations, such as inserting data somewhere other than the start of the document, replacing certain data with new data, or even deleting certain data from the document.

### Merging into TXT Files

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

Merging into JSON files is done using a [JSON Patch](https://jsonpatch.com/) document.

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

We can modify the above data with a document `mods/mymod/_append/data/songs/mysong-metadata.json`:

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
