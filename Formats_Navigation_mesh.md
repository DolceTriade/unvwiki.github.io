---
title: Formats Navigation mesh
permalink: /Formats/Navigation_mesh/
---

The game supports automatic navigation mesh generation from map files.
This (or "navmesh" for short) is used by the bots to navigate throughout
the world.

The navigation mesh format is game-specific (mods may modify it).

## Using a navigation mesh

Navigation mesh files go in the `maps/` directory either in the folder
specified by the `fs_game` cvar, or in the maps folder inside a map's
file.

## Testing the mesh

- You may test your map locally by entering
  `\devmap `<var>`mapName`</var> as you would to test any map at any
  time. Note, of course, that this will disconnect you from whatever
  game you may currently be in.
- To enable drawing the navigation mesh, use
  `navedit enable navmeshname` where "navmeshname" is one of:

<!-- -->

- human_naked
- human_bsuit
- builder
- builder-upg
- level0
- level1
- level1upg
- level2
- level2upg
- level3
- level3upg
- level4

Where level4 is tyrant, level3 is dragoon, level2 is marauder, level1 is
mantis, and level0 is dretch. The two builder navmeshes are not used at
this time.

- Add bots with the `bot` command and spectate the game.

## Editing the navigation mesh

Navmesh editing is still a work in progress, but it can be useful for
fixing unnavigable ledges.

Unfortunately, automatic navigation mesh generation that fully supports
all of the map features and player abilities in Unvanquished is
incredibly difficult. Automatic generation will usually produce a very
satisfactory base mesh, but some areas may need further tweaking.

To edit the navmesh, you must select the one you wish to edit using the
`navedit` command.

To add connections use the `addcon` command.

A oneway connection will only allow bots to move from the start of the
connection to the end of the connection, but not from the end to the
start. A twoway connection will allow bots to move in either direction
along the connection. The radius of the connection is how far away the
center of the bot has to be from the middle to take the connection.

Modifications to the navmesh are made in real time, so any bots that
have spawned will react accordingly.

When you are done editing a specific navmesh, you can use `navedit save`
to save your work.

## Research

Slides and demo code of a talk in which someone presented a way to get
covers and jump links handled:

- <http://digestingduck.blogspot.com/2011/07/paris-gameai-conference-2011-slides-and.html>

[Category:Formats](Category:Formats "wikilink")
[Category:Mapping](Category:Mapping "wikilink")
[Category:Bots](Category:Bots "wikilink")