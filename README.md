ItDR Core
=========

Core LaTeX packages for the [Into the Dungeon: Revived](https://vladar4.github.io/itdr/) role-playing game and compatible materials.

Usage
-----

Consult the [manual](MANUAL.md) and `itdr-core-guide.tex` document for the list of available commands and practical examples of their usage.

The compiled PDF version of `itdr-core-guide` is available in [Releases](https://github.com/Vladar4/itdr-core/releases).

Packages
--------

- [core.sty](MANUAL.md#core.sty) — the main package that provides everything you need to produce a document in ItDR style.

- [bestiary.sty](MANUAL.md#bestiary.sty) — the expandable CSV bestiary database that allows you to insert previously defined monster stat-blocks using short LaTeX commands.

Dependencies
------------
[TeX Live](https://www.tug.org/texlive/)

### Arch
`sudo pacman -S texlive-bin texlive-binextra texlive-basic texlive-plaingeneric texlive-fontsrecommended texlive-fontsextra texlive-latex texlive-latexrecommended texlive-latexextra`

### Debian
`sudo apt-get install texlive-latex-base texlive-fonts-extra texlive-latex-extra`

Changelog
---------

### 2024-04-20
- Added new commands:
    - `\rot` and `\iconrot` for icon rotation
- Added new custom icon: `\iconCorridor`
- Added various arrow icons
- Improved `\dimensions` command

### 2024-04-14
- Added new command: `\pcell`
- Better margins for boxes and tables

### 2024-04-12

#### core.sty
- Added new environment: `\cbox`
- `\placeholder` command - added vertical dimension printout
- `\room` command regression fix
- List formatting - changed to `\setlist` call

#### bestiary.sty
- Leech swarm - non-Blast attacks are Impaired

### 2023-12-18

#### core.sty
- Added starred version of `\chapterx` command
- Removed TOC indentation for unnumbered chapters

#### bestiary.sty
- `\bestiaryPrintAllEntries` command now has an optional `fields` argument
- Added range printing commands:
    - `\bestiaryPrintNamesRange`
    - `\bestiaryPrintNamesRangeByTag`
    - `\bestiaryPrintEntriesRange` and `\bestiaryPrintEntriesRange*`
    - `\bestiaryPrintEntriesRangeByTag` and `\bestiaryPrintEntriesRangeByTag*`

### 2023-12-01
Initial release.

