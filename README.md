ItDR — Core
===========

Core LaTeX packages for the [Into the Dungeon: Revived](https://vladar4.github.io/itdr/) role-playing game and compatible materials.

Usage
-----

Add this repository as a submodule into your git project, or just put its contents into the `itdr` sub-directory.

```
git submodule add https://github.com/Vladar4/itdr-core itdr
git commit -m 'Added itdr-core submodule'
git push
```

Consult the `itdr-core-guide.tex` document for the list of available commands and practical examples of their usage.
The compiled PDF version of `itdr-core-guide` is available in [Releases](https://github.com/Vladar4/itdr-core/releases).

Packages
--------

### core.sty

`\usepackage{itdr/core}`

The main package that provides everything you need to produce a document in ItDR style.

### def.tex

Create one for your project, using the example presented here, and input it in your project's preamble (`\input{def}`) just before `\begin{document}`.

```tex
\def \game {Into the Dungeon: Revived}	% GAME variable
\def \title {Title}	% TITLE variable
\def \subtitle {Subtitle}	% SUBTITLE variable
\def \author {Author}	% AUTHOR variable
\def \keywords {\title;Into the Dungeon;RPG}	% KEYWORDS variable
\def \version {v1.0}	% VERSION variable
\def \license {\href{https://creativecommons.org/licenses/by-sa/4.0/}{Creative Commons Attribution-ShareAlike 4.0 International License (CC BY-SA 4.0)}}	% LICENSE variable
```

### bestiary.sty

`\usepackage{itdr/bestiary}`

The expandable CSV bestiary database that allows you to insert previously defined monster stat-blocks using short LaTeX commands.

Dependencies
------------
[TeX Live](https://www.tug.org/texlive/)

### Arch
`sudo pacman -S texlive-bin texlive-binextra texlive-basic texlive-plaingeneric texlive-fontsrecommended texlive-fontsextra texlive-latex texlive-latexrecommended texlive-latexextra`

### Debian
`sudo apt-get install texlive-latex-base texlive-fonts-extra texlive-latex-extra`


Changelog
---------

### 2023-12-01
Initial release.

