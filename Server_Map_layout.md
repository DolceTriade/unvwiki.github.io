---
title: Server Map layout
permalink: /Server/Map_layout/
---

Map layouts store alternate starting positions of buildables.

If your want **create layouts in the game**, you can easily follow this
page : [Map_Layouts](Map_Layouts "wikilink")

## Saving layouts

Layouts are saved with the `layoutsave` command:

`/layoutSave `<var>`filename`</var>

Layout files are written to
`layouts/`<var>`mapname`</var>`/`<var>`filename`</var>`.dat`.

Layout files are plain-text and have one line per buildable. The syntax
is as follows:

<var>`name`</var>` `<var>`pos`</var>` `<var>`angles`</var>` `<var>`origin2`</var>` `<var>`angles2`</var>

- <var>name</var> may be one of `eggpod`, `overmind`, `barricade`,
  `acid_tube`, `trapper`, `booster`, `hive`, `telenode`, `mgturret`,
  `rocketpod`, `arm`, `medistat`, or `reactor`.
- <var>pos</var>, <var>angles</var>, <var>origin2</var>, and
  <var>angles2</var> are all space-delimited triples of position or
  angle data, and the meaning of each is dependent on the particular
  buildable with the exception of <var>pos</var>, which is the world
  position of the buildable.

## Choosing a layout file

Layouts may be specified in map rotation files.

The current selection of layouts is indicated by `g_layouts`.

- `/changemap `<var>`map`</var>` [`<var>`layout`</var>`]` Changes the
  map to <var>map</var> and sets the current layouts to
  <var>layout</var>. Note that with this command, only one layout may be
  specified.
- `/callvote layout [`<var>`layout`</var>`]` Calls a vote to restart the
  game with the layout <var>layout</var>.

A list of layouts available for the current map may be seen with
`/listlayouts`.

[Category:Server](Category:Server "wikilink")
[Category:Formats](Category:Formats "wikilink")