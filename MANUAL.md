ItDR Core Manual
================

- [Project structure](#project-structure)
    - [def.tex](#deftex)
    - [project.tex](#projecttex)
    - [part0.tex](#part0tex)
- [core.sty](#coresty)
    - [Boxes](#boxes)
    - [Fonts](#fonts)
    - [Footnotes](#footnotes)
    - [Icons](#icons)
    - [Images](#images)
    - [Index](#index)
    - [Lists](#lists)
    - [Sectioning](#sectioning)
    - [Tables](#tables)
    - [Templates](#templates)
    - [Table of contents](#table-of-contents)
    - [Wrap](#wrap)
    - [Hyperlinks](#hyperlinks)
- [bestiary.sty](#bestiarysty)
    - [Fields](#fields)
    - [Management](#management)
    - [Usage](#usage)

---

Project structure
-----------------

Add this repository as a submodule into your git project, or just put its contents into the `itdr` sub-directory.

```
git submodule add https://github.com/Vladar4/itdr-core itdr
git commit -m 'Added itdr-core submodule'
git push
```

The minimal viable project structure:

```
project
├── itdr
│   ├── bestiary.csv
│   ├── bestiary.sty
│   ├── core.sty
│   ├── img
│   │   ├── bottom_line_even.pdf
│   │   ├── bottom_line_odd.pdf
│   │   ├── box_bottom.pdf
│   │   ├── box_quote.pdf
│   │   ├── box_top.pdf
│   │   ├── itdr_link.pdf
│   │   └── itdr_logo.pdf
│   └── itdr.ist
├── def.tex
├── part0.tex
├── part1.tex
├── ...
└── project.tex
```

---

### def.tex

This file defines the main variables and metadata for the PDF file.

Follow the example below to create your `def.tex` and input it in your project's preamble (`\input{def}`) just before `\begin{document}`.

```tex
\def \game {Into the Dungeon: Revived}	% GAME variable
\def \title {Title}	% TITLE variable
\def \subtitle {Subtitle}	% SUBTITLE variable
\def \author {Author}	% AUTHOR variable
\def \keywords {\title;Into the Dungeon;RPG}	% KEYWORDS variable
\def \version {v1.0}	% VERSION variable
\def \license {\href{https://creativecommons.org/licenses/by-sa/4.0/}{Creative Commons Attribution-ShareAlike 4.0 International License (CC BY-SA 4.0)}}	% LICENSE variable
```

---

### project.tex

This is the main project file. Rename it to represent your project.

```tex
\documentclass[10pt,twoside,twocolumn,openany]{book}
\usepackage[utf8]{inputenc}
\usepackage[british]{babel}
\usepackage{subfiles}
\usepackage{itdr/core}%     <- required
\usepackage{itdr/bestiary}% <- optional

\input{def}% variables

\begin{document}
\fontfamily{ppl}\selectfont % Set text font

\begin{titlepage}
\newgeometry{margin=1in,top=1.1in}
\begin{onecolumn}

% TITLE
\begin{center}
	\textBigTitle{\title}\\
	\hrule\vspace{2ex}
	\textSubTitle{\subtitle}\\
\end{center}

\vspace{-2ex}
\vfill

% COVER IMAGE
\dimage{cover}{468pt}

\vfill

% FOOTNOTE
\noindent\hspace{-0.75em}\begin{minipage}{0.15\textwidth}
\centering\includegraphics[width=\linewidth]{itdr_logo.pdf}
\end{minipage}\hspace{-0.45em}\begin{minipage}{0.7\textwidth}
{\begin{center}\footnotesize
\href{https://vladar4.github.io/itdr/}{``\title''} by \author{}\\
is designed to be used with ``Into the Dungeon: Revived'' ruleset freely available at\\
\href{https://vladar4.github.io/itdr}{https://vladar4.github.io/itdr} and \href{https://vladar.itch.io/into-the-dungeon-revived}{https://vladar.itch.io/into-the-dungeon-revived}.

% VERSION AND YEAR
\vspace{\baselineskip}
\small\version\\\year
\end{center}
}\end{minipage}\hfill\begin{minipage}{0.15\textwidth}
\centering\includegraphics[width=\linewidth]{img/itdr_link.pdf}
\end{minipage}\hspace{0.5em}

\end{onecolumn}\end{titlepage}
\restoregeometry
\clearpage

% SUBFILES
\subfile{part0}	% Introduction
\subfile{part1}	% Chapter 1
% ...

\end{document}
```

---

### part0.tex

```tex
\documentclass[itdr/core]{subfiles}

\begin{document}

\toc[2] % Table of Contents

\vfill

\noindent
\begin{minipage}{\textwidth}
\begin{center}\fnsize
	Writing and illustrations by \author{}.

	``\title'' is licensed under\\the \license.
\end{center}
\end{minipage}

\clearpage

\chapterx{Introduction}
\label{ch:introduction}

\end{document}
```

---
---

core.sty
--------

The main package that provides everything you need to produce a document in ItDR style.

`\usepackage{itdr/core}`

### Boxes

#### dbox environment

"Default" box — optional rules and notes.

#### abox environment

"Aloud" box — room descriptions and other material to read aloud to the players.

#### qbox environment

"Quote" box — quotes and handouts.

#### cbox environment

"Centered" box — same as `qbox`, but for short quotes and handouts.
This box can be shorter than `\linewidth`.

#### bbox environment

"Background" box — highlighting important information.

#### lbar environment

Left bar — vertical bar to the left side of the text, used in [Domain](#domain) command.

#### rightbox

`\rightbox[\parskip]{text}`

Put a right-aligned line of text raised by `\baselineskip + #1`.

Default of `#1` is `\parskip` to put the text on a `\paragraph{}` line above.

#### righttext

`\righttext{text}`

Right-aligned text.

---

### Fonts

#### docFontSize

`\docFontSize`

Document font size length, used in some calculations.

#### fancyfont

`\fancyfont`

Fancy font used for `\textBigTitle` and `textSubTitle`.

#### textBigTitle

`\textBigTitle[size][baselineskip]{text}`

Print book title.

#### textSubTitle

`\textBigTitle[size][baselineskip]{text}`

Print book subtitle.

---

### Footnotes

#### fnsize

`\fnsize`

Footnote font size (`small` by default)

#### note

`\note[n]`

Print `n`-th footnote symbol for a local note.

#### notetext

`\notetext[n]{text}`

Print `n`-th local note `text`.

---

### Icons

#### iconItDR

`\iconItDR`

Custom ItDR logo icon

#### faCorridor

`\faCorridor`

Custom corridor icon based on `\faDungeon`

#### faOldKey

`\faOldKey`

Custom old key icon (from fontawesome v4)

#### iconLower

`\iconLower`

Vertical kerning length for icons.

#### icon

`\icon{\icon}`

Print an icon at the start of the line without indentation.

#### icontitle

`\icontitle{\icon}{\title}{Text}`

Print an icon at the start of the `\title` (`\section`, `\paragraph`, etc.)

#### Arrows

Each set of arrows (except `Arrows` and `Level` ones) has eight versions for all cardinal directions: `N`, `NE`, `E`, `SE`, `S`, `SW`, `W`, `NW`.

- `Arrows`:
    - `\iconArrows` - "plus-shaped" cross of arrows
    - `\iconArrowsX` - "x-shaped" cross of arrows
    - `\iconArrowsV` - "vertical" arrow pointing up and down
    - `\iconArrowsH` - "horizontal" arrow pointing left and right
    - `\iconArrowsS` - "slash" arrow pointing bottom-left and top-right
    - `\iconArrowsB` - "backslash" arrow pointing top-left and bottom-right
- `Arrow` - a set of eight normal arrows (`\iconArrowN`, `\iconArrowNE`, etc.)
- `ArrowCircle` - a set of eight arrows in a black circle (`\iconArrowCircleN`, `\iconArrowCircleNE`, etc.)
- `ArrowAltCircle` - a set of eight arrows in a white circle (`\iconArrowAltCircleN`, `\iconArrowAltCircleNE`, etc.)
- `Chevron` - a set of eight chevrons (`\iconChevronN`, `\iconChevronNE`, etc.)
- `ChevronCircle` - a set of eight chevrons in a black circle (`\iconChevronCircleN`, `\iconChevronCircleNE`, etc.)
- `Level`:
    - `iconLevelUp` - bent arrow pointing up
    - `\iconLevelDown` - bent arrow pointing down

#### Shortcuts

- `\def\iconBookmark{\faBookmark}`
- `\def\iconContainer{\faCube}`
- `\def\iconCorridor{\faCorridor}`
- `\def\iconCharacter{\faUser}`
- `\def\iconDay{\faSun}`
- `\def\iconGroup{\faUsers}`
- `\def\iconSize{\faRulerCombined}`
- `\def\iconDanger{\faSkullCrossbones}`
- `\def\iconDirections{\faMapSigns}`
- `\def\iconDoor{\faDungeon}`
- `\def\iconEncounter{\faExclamationTriangle}`
- `\def\iconHidden{\faSearch}`
- `\def\iconKey{\faOldKey}`
- `\def\iconLock{\faLock}`
- `\def\iconMagic{\faMagic}`
- `\def\iconMonster{\faDragon}`
- `def\iconMoon{\faMoon}`
- `\def\iconNight{\faMoon}`
- `\def\iconReward{\faTrophy}`
- `\def\iconStar{\faStar}`
- `\def\iconSun{\faSun}`
- `\def\iconTimer{\faHourglassHalf}`
- `\def\iconTravel{\faHiking}`
- `\def\iconTreasure{\faGem}`
- `\def\iconTrigger{\faBolt}`
- `\def\iconVisible{\faEye}`

---

### Images

The default `\graphicspath` is:
`{./img/} {./img/pic/} {./pic/} {./itdr/img/}`

#### placeholder

`\placeholder[width]{filename}{height}`

- `width` - *(optional)* default: `\linewidth`
- `filename` - placeholder text
- `height` - placeholder height

Used internally to display a placeholder of non-existing `\dimage`.

#### dimage

`\dimage[options]{filename}[extension]{height}`

- `options` - *(optional)* `\includegraphics` options (`width=\linewidth,#1` by default)
- `filename` - image file name
- `extension` - `(optional)` default: `png`
- `height` - expected image height (for `\placeholder`)

The default command for image inclusion.
Dimensions `\linewidth` x `height`

#### dimagebottom

`\dimagebottom[options]{filename}[extension]{height}`

- `options` - *(optional)* `\includegraphics` options (`width=\textwidth,#1` by default)
- `filename` - image file name
- `extension` - `(optional)` default: `png`
- `height` - expected image height (for `\placeholder`)

A full-page image at the bottom of the page.
Place **BEFORE** anything on the page.
Dimensions: `\textwidth` x `height`.

#### dimagepage

`\dimagepage[options]{filename}[extension]`

- `options` - *(optional)* `\includegraphics` options (`width=\textwidth,#1` by default)
- `filename` - image file name
- `extension` - `(optional)` default: `png`

A full-page image on a separate page (`\thispagestyle{empty}`).
Dimensions: `\textwidth` x `636pt`.

---

### Index

#### newindex

`\newindex{name}{title}`

Initialize a new index.
It's style is defined in `itdr/itdr.ist` file and can be overriden by creating `itdr.ist` file in the project's root directory.

---

### Lists

#### itemrange

`\itemrange{range}`

Enumerate list index with range of values.
E.g., `\itemrange{3} second item` will produce `2–4. second item`.

---

### Sectioning

#### tocstep

`\tocsep`

"Tabbing" step distance for TOC, used internally.

#### New title classes

- `\chapterx` - unnumbered chapter
- `\chapterx*` - unnumbered chapter without a TOC entry
- `\paragraphsection` - a new title class between `\subsubsection` and `\paragraph`.
- `\paragraphsubsection` - a new title class between `\paragraph` and `\subparagraph`.

---

### Tables

#### New column types

- `L` - left-aligned column
- `C` - centered column
- `R` - right-aligned column

#### header

`\header{Text}`

Table header.

#### dtable environemnt

The default table (`tabularx`) of `\linewidth` width.
Takes a single argument of columns specification (default: `LL`).

#### pcell

`\pcell[width]{contents}[linespread]`

A wrapper of `\pbox` to use inside tabular cells, with custom linespread.

- `width` - *(optional)* maximum paragraph width (`\linewidth` by default)
- `contents` - paragraph contents
- `linespread` - *(optional)* custom linespread factor (`0.5` by default)

---

### Templates

#### cleartoleftpage

`\cleartoleftpage`

Start from a new left (even) page.

#### tsub

`\tsub{text}`

A shorthand for `\textsubscript`.

#### tsup

`\tsup{text}`

A shorthand for `\textsuperscript`.

#### dbar

`\dbar`

A prettier double bar glyph.

#### skipline

`\skipline[length]`

- `length` - *(optional)* vertical skip length (`\baselineskip` by default)

A shorthand for `\vspace*{length}`.

#### tight

`\tight`

A shorthand for `\looseness=-1`.
When placed at the end of a paragraph, it attempts to fit the text in a lesser amount of lines than previously.

#### Saves

- `\save{ABILITY}` = "ABILITY~Save"
- `\saves{ABILITY}` = "ABILITY~Saves"

📝 **NOTE:** Starred templates do not push names to the `index` (`\jobname` by default), while the default ones do. In both cases, they add to the TOC at `paragraph` level.

#### Feats

- `\feat[index]{name}` and `\feat*{name}` - feature header
- `\feata[index]{name}` and `\feata*{name}` - ancestry header
- `\featb[index]{name}` and `\featb*{name}` - background header
- `\featmt` = "Can be taken multiple times."
- `\feathp` = "Roll twice for HP and take the better result."
- `\feate{Text}` = "Eligibility: Text"
- `\featadv` = "Advancement:"

#### Equipment

- `\equip[index]{name}{price}` and `\equip*{name}{price}` - equipment template
- `\weapon[index]{name}{price}{damage}` and `\weapon*{name}{price}{damage}` - weapon template
- `\armour[index]{name}{price}{value}` and `\armour*{name}{price}{value}` - armour template

#### Domains

- `\sizpop[populace]{siz}` - print domain size along with appropriate populace. If `populace` argument is present, it overrides the default populace value.
- `\domain{ruler}{siz}[populace]{details}` - domain info template.

#### Spells

Default spell index should be defined as `\newindex{\spells}{Spell List}` before the start of your document. `\spells` is it's pre-defined name.

📝 **NOTE:** Define `\def \spellcircle {X}` (where `X` is `C`, `1`, `2`, `3`, `4`, or `5`) before calling the `\spell` or `\spell*` command.

- `\spell[index]{name} description` and `\spell*{name} description` - spell paragraph
- `\sspell[index]{name}{circle}` and `\sspell*{name}{circle}` - standalone spell paragraph (does not need the `\spellcircle` being defined)

#### Rooms

`\room[\title]{idx}{name}`

- `\title` - *(optional)* title level (`\subsection` by default)
- `idx` - the map index of the room (two-line lettrine)
- `name` - the name of the room

Room header with two-line lettrine of its index on the map.

`\dimensions[unit]{x}{y}[z]`

- `unit` - *(optional)* measure unit (`~ft.` by default)
- `x`, `y` - horizontal dimensions
- `z` - *(optional)* vertical dimension

Room dimensions to use immediatelly after the `\room` command.

#### Paragraphs

- `\iparagraph[index]{title}` - indexed paragraph; adds to the default index (`\jobname`) by default
- `\statpar[index]{monster name}` and `\statpar*{monster name}` - monster stat block header
- `\underpar{text}` - monster stat block underparagraph (sub-header)

#### Classess and Creeds

📝 **NOTE:** Legacy commands used in [Classic Appendix](https://github.com/Vladar4/itdr-classic/).

- `\class[index]{name}` and `\class*{name}` - class header
- `\creed[index]{name}` and `\creed*{name}` - creed header

#### Miscellaneous

- `\travelunit{distance}` - convert travel distance in 5-mile hexes to miles
- `\dnotes[4ex]` - fill the page with equally-distanced lines

---

### Table of contents

`\toc[level]`

Print out the table of contents of the `level` depth:
- `\toc[0]` - `\chapter` depth
- `\toc[1]` - `\section` depth
- `\toc[2]` - `\subsection` depth
- `\toc[3]` - `\subsubsection` depth
- `\toc[4]` - `\paragraphsection` depth
- `\toc[5]` - `\paragraph` (and `\iparagraph`) depth
- `\toc[6]` - `\paragraphsubsection` depth
- `\toc[7]` - `\subparagraph` depth

---

### Wrap

`\begin{wrap}[line number]{location}{overhang}{width}`

Wrapped paragraph environment. See [wrapfig2](https://www.ctan.org/pkg/wrapfig2) documentation for details.

---

### Hyperlinks

- `\customref{label}{text}` - custom reference link to the `label`
- `\roomref{room}` - reference link to [rooms](#Rooms) by title (e.g. `\roomref{1. First Room}` will refer to the `\room{1}{First Room}`)
- `\fullref{label}` - full reference link to the `label`
- `\safenameref{label}[fallback]` - if the label is undefined, `fallback` is printed instead
- `\safepageref{before}{label}{after}[fallback]` - page link between `before` and `after` text; if the label is undefined, `fallback` is printed instead

---
---

bestiary.sty
------------

The expandable CSV bestiary database that allows you to insert previously defined monster stat-blocks using short LaTeX commands.

`\usepackage{itdr/bestiary}` - load with the default database file (`itdr/bestiary`)

`\usepackage[db=filename]{itdr/bestinary}` - load with a custom database file

`\usepackage[db={file1, file2, file3, ...}]{itdr/bestiary}` - load with a custom list of database files

---

### Fields

```
% bestiary.csv database fields (separated by | character):
%
% 	       |-----------stat-----------|    |--info--(upt to 10 info fields)
%          |                          |    |
% 1   |2   |3  |4  |5  |6 |7     |8   |9   |10     |
%     |    |   |   |   |  |      |    |    |       |
% name|tags|str|dex|wil|hp|armour|data|desc|info(1)|...
```

- `name` - monster name
- `tags` - comma-separated list of tags (`beast`, `construct`, `demon`, `dragon`, `monster`, `swarm`, `undead`, etc.)
- `str`, `dex`, `wil` - ability scores, `10` by default
- `hp` - hit points
- `armour` - armour score and description, if needed, e.g.: `2 (piecemeal armour + shield)`
- `data` - the rest of the first line of a stat block: attacks, abilities, etc.
- `desc` - literary description paragraph
- `info` - ten fields for the abilities and properties descriptions

Example:

```
name|tags|str|dex|wil|hp|armour|data|desc|info||
Elephant|beast|20||8|12|1|d10~Tusks||\subparagraph{Charge:} a target must pass a \save{DEX} or take Tusks Damage and be knocked prone.|\subparagraph{Trample:} a prone target takes d12~Damage.|
```

---

### Management

- `\bestiaryDefault` - default database file name (`itdr/bestiary` by default)
- `\bestiaryExtension` - database file extension (`csv` by default)
- `\bestiaryFilename{filename}` - add the file extension to a file name (done automatically on load)
- `\def\bestiaryIndex{index}` - set or disable *(default)* the bestiary index
- `\bestiaryClear` - clear the database
- `\bestiarySort` - sort database by name field
- `\bestiaryLoad{filename}` - clear, load and sort the database by name field
- `\bestiaryAppend{filename}` - append to the database and sort it by name field
- `\bestiaryLoadList{file1, file2, file3, ...}` - clear the database, load a comma-separated list of files, and then sort it by name field
- `\DTLdef{\name}{bestiaryDB}{column1 name}{column1 value}{column2 name}` - store the value of `column2` into a new `\def`

---

### Usage

📝 **NOTE:** For all optional `fields` arguments below, the default value is `name,stat,desc,info` (the whole entry).

#### Print an Entry

- `\bestiaryPrint[fields]{name}` - print a single entry, or just some of its `fields` (comma-separated)
- `\bestiaryPrint*[fields]{name}` - same but do not add into the bestiary index
    - `\bestiaryPrintField{name}{field}` - print a single `field` of an entry
    - `\bestiaryPrintStat{name}` - print and format stat fields of an entry
    - `\bestiaryPrintDesc{name}` - print a `desc` field of an entry
    - `\bestiaryPrintInfo{name}` - print all info fields of an entry

#### Print Names

- `\bestiaryPrintNamesByTag{tag}[prefix][suffix]` - print all names containing a specific `tag` with an optional `prefix` and `suffix`
- `\bestiaryPrintNamesRange{first}{last}[prefix][suffix]` - print names in range from `first` to `last` one, with an optional `prefix` and `suffix`
- `\bestiaryPrintNamesRangeByTag{first}{last}{tag}[prefix][suffix]` - print names containing a specific `tag` in range from `first` to `last` one, with an optional `prefix` and `suffix`
- `\bestiaryPrintAllNames[prefix][suffix]` - print all names from the database with an optional `prefix` and `suffix`

#### Print Entries

- `\bestiaryPrintEntriesByTag[fields]{tag}[before][after]` - print all entries (or just some `fields`) containing a specific `tag` with an optional `before` and `after` text for each entry
- `\bestiaryPrintEntriesByTag*[fields]{tag}[before][after]` - same, but do not add into the bestiary index
- `\bestiaryPrintEntriesRange[fields]{first}{last}[before][after]` - print entries (or just some `fields`) in range of names from `first` to `last` one, with an optional `before` and `after` text for each entry
- `\bestiaryPrintEntriesRange*[fields]{first}{last}[before][after]` - same, but do not add into the bestiary index
- `\bestiaryPrintEntriesRangeByTag[fields]{first}{last}{tag}[before][after]` - print entries (or just some `fields`) containing a specific `tag` in range of names from `first` to `last` one, with an optional `before` and `after` text for each entry
- `\bestiaryPrintEntriesRangeByTag*[fields]{first}{last}{tag}[before][after]` - same, but do not add into the bestiary index
- `\bestiaryPrintAllEntries[before][after][fields]` - print all entries (or just some `fields`) from the database with an optional `before` and `after` text for each entry
- `\bestiaryPrintAllEntries*[before][after][fields]` - same, but do not add into the bestiary index

---
---

