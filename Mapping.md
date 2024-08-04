---
title: Mapping
permalink: /Mapping/
---

Mapping or 'level-making' for Unvanquished is fun to learn but difficult
to master. Creating maps is highly open ended — anyone can use any of an
infinite variety of techniques to make a map, for both fun and showing
off via release.

This page provides resources and tutorials for all skill levels, from
beginner to demi-goat.

## Getting Started

- [Getting started with
  NetRadiant](Tutorials_Getting_started_with_NetRadiant "wikilink") —
  installing and setting up the mapping tools
- [Level editors](Tools_Level_editors "wikilink") — Comparison of level
  editors.
- [Mapping tools](Tools_Mapping "wikilink") — List of mapping tools.
- [Mapping guide](Tutorials_Mapping_guide "wikilink") — From start to
  finish, assuming little previous knowledge.
- [Tremulous Mapping
  Tutorial](http://tremmapping.pbworks.com/w/page/22453200/Starting%20Tremulous%20Mapping)
  — still applicable to Unvanquished
- [Map testing hints](Testing_Maps "wikilink")

## Techniques and Features

- [Colour Grading](Tutorials_Colour_Grading "wikilink") — Changing
  colour-schemas
- [Reverberation](Tutorials_Reverberation "wikilink") — Testing and
  adding reverberation effects (natural sound echo)
- [Minimaps](Tutorials_Minimap "wikilink") — Current minimap system.
  Will eventually be replaced with automatic model.

## Mapping Approaches

- [Modular
  environments](http://www.thiagoklafke.com/modularenvironments.html) —
  making maps out of pre-made components

## VIS and optimisation

Unvanquished employs a VIS (visibility) system to improve game
performance. Only a visible subset of a whole levels is 'rendered' at
any one time, because rendering things you can't see wastes performance.
Although the compiler can do this itself, more efficient VIS systems can
be enforced by doing it by hand.

- [Understanding Vis and Hint
  Brushes](http://tremmapping.pbworks.com/w/page/22453205/Understanding%20Vis%20and%20Hint%20Brushes)
- [Advanced VIS and hinting
  tutorial](http://www.quake3world.com/forum/viewtopic.php?t=3620)

## Compilation

Maps must be compiled by a compiler to get them into a format the
[engine](Daemon "wikilink") understands.

- [Compilation overview](Mapping_Compilation "wikilink")
- [Wikipedia article on 'Quake
  Engine'](https://en.wikipedia.org/wiki/Quake_engine) — brief
  description of map mesh optimisation.

## Migrating content from other quake engines

- [Entity Changes](Entities_Changes "wikilink") — entity changes from
  Tremulous and Q3

## Old guides

Content in these should either be used in new guides or updated to be
useful.

- [Old mapping page](Old_Mapping "wikilink") — old mapping page, some
  content has still not been merged.

## Design with bots in mind

Unvanquished supports bot players, but those have rather limited
intelligence. While mapping, it might be a oood idea to keep in mind
that when there are bots, they might completely break balance if they
are too dumb to take some paths. While it is hoped that their brain will
be improved, some commands can help debugging and improving their
behaviors.

- — View navmeshes.

[Category:Mapping](Category:Mapping "wikilink")