# Writing And Contributing to This Book
This book is written in Markdown format, and uses [mdbook](https://rust-lang.github.io/mdBook/) for generation.

The source files from which this book is generated can be found on [GitHub](https://github.com/FunkinCrew/funkin-modding-docs).

## Things to Consider

- How should we handle explaining directory paths? The source code has some of the 
assets split into libraries (`preload/`, `songs`, `shared`, etc.) however most people modding don't need to
really mind the source code versions of asset paths. 
- Currently [Chapter 10: Appending and merging Files](10-appending-and-merging-files/10-00-appending-and-merging-files.md) renders as "Chapter 5"

### Style Guide

#### Folder/Chapter Structure

[SUMMARY.md](SUMMARY.md) is how `mdbook` generates the chapters, sub-chapters, of all the markdown files. In there you can see how the book is laid out in terms of it's content. 

Folder structure is entirely independant from content ordering, so we can organize generally how we please as long as [SUMMARY.md](SUMMARY.md) is pointing to the right files.

Folder names should be `{chapter number}-{chapter title}`, generally despite how long the `chapter title` may end up being
From this guides source:
```shell
src/
    01-fundamentals/
    02-custom-songs-and-custom-levels/
    03-custom-characters/
    ... // and so on...
```

The main chapter page should be `{chapter number}-00-{chapter title}.md` in the chapter's folder.
From this guides source:
```shell
src/
    01-fundamentals/
        01-00-fundamentals.md
        ...

    02-custom-songs-and-custom-levels/
        02-00-custom-songs-and-custom-levels.md
        ...
    ...
```

Then each successive sub-chapter should follow `{chapter number}-{sub-chapter number}-{subchapter title}.md`
From this guides source:
```shell
src/
    01-fundamentals/
        01-00-fundamentals.md
        01-01-the-metadata-file.md
        01-02-loading-the-mod-in-game.md
        ...

    02-custom-songs-and-custom-levels/
        02-00-custom-songs-and-custom-levels.md
        02-01-creating-a-chart.md
        02-02-adding-the-custom-song.md
        02-03-adding-a-custom-level.md
    03-custom-characters/
        03-00-custom-characters.md
        03-01-character-assets.md
        ...
    ...
```




