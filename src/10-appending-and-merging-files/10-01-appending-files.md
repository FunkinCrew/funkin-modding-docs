# Appending Files

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

If you want something more particular, see [Merging into JSON Files](./10-02-merging-files.md#merging-into-json-files) for a more powerful and flexible approach.
