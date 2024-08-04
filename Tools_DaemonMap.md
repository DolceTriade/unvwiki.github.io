---
title: Tools DaemonMap
permalink: /Tools/DaemonMap/
---

DæmonMap was a tool to generate files for game levels from files.

Starting with Unvanquished 0.54.0 the navmesh generator is built in the
game itself so there is no need anymore to use an external tool.

## Sources

The DaemonMap source repository is
[github.com/DaemonEngine/daemonmap](https://github.com/DaemonEngine/daemonmap).

The tool is a fork of [Q3map2](Tools_Q3map2 "wikilink") focused on
generating navmeshes (everything else has been stripped out).

## Features

The tool was able to generate navigation meshes for Unvanquished maps
(id Tech 3 BSP format).

## No future

This tool has been replaced by in-game navmesh generation and is now
obsolete. It has no future.

## Generating a Navigation mesh

The `-nav` parameter to will generate a navigation mesh from a file.

Use it like so:

### Windows

`daemonmap.exe -game unvanquished -nav mapname.bsp`

### Linux/macOS

`daemonmap -game unvanquished -nav mapname.bsp`

### Optional parameters

The navigation mesh generation process is conservative by default. This
means some areas (particularly, small ledges) that should be walkable
may instead create a break in the navmesh which bots interpret as "I am
unable to go past there." The following optional parameters give the map
maker some control over navmesh generation to help with this.

- `-cellheight`
  A lower cellheight will increase mesh generation accuracy at the cost
  of generation time and mesh size.

  If there are gaps in the navigation mesh even though a player can
  easily just walk to get through, you can decrease the value to help.
- `-median`
  Applies a median filter to the walkable areas of the mesh to help
  contain any "noise."

  See [this
  article](http://digestingduck.blogspot.com/2010/07/recast-area-types-per-triangle.html)
  for more information.
- `-optimistic`
  Attempts to compensate for cellsize inaccuracy by increasing the
  stepheight navigation mesh generation parameter based on the current
  samplesize. It is recommended to be used with a lower than default
  cellsize to help avoid over optimistic assumptions (i.e., saying some
  areas are walkable that really aren't). Useful for fixing breaks in
  the mesh caused by some small ledges.

  This produces bad results depending on how big your `cellsize`
  parameter is, but generating the mesh in this way will be faster than
  simply decreasing the `cellheight`.

[Category:Tools](Category:Tools "wikilink")
[Category:Mapping](Category:Mapping "wikilink")