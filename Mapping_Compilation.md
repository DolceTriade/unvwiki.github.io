---
title: Mapping Compilation
permalink: /Mapping/Compilation/
---

Maps must be compiled from editor formats used to make them (eg , ) into
a format the game understands (.bsp). This process has many stages and
can take some time — from seconds for simple maps to hours for very
large and complex maps.

Unvanquished currently uses Q3Map2 for normal map compilation (included
with NetRadiant).

# Space Partitioning

Map geometry is subdivided (partitioned) in half successively,
effectively breaking the map down into progressively smaller chunks. The
reason for this is to improve in-game render speed; this is done in such
a manner that the engine can quickly determine what portions of the map
the player is not facing, and therefore avoid having to render such
areas. The scheme by which this is done is referred to as [binary
spatial
partitioning](http://en.wikipedia.org/wiki/Binary_space_partitioning),
and this (as well as the data structure storing this information) is
most often referred to as BSP. With each split, the compiler attempts to
minimize the amount of geometry that must be cut to minimize the
resulting size of the BSP.

# Potentially Visible Set (PVS) calculation

<http://en.wikipedia.org/wiki/Potentially_visible_set>

This stage of compilation adds another speed boost atop that which BSP
provides by calculating which regions of the map are visible when viewed
from other areas so that areas that are not visible are not drawn. Each
of these areas for which a potentially visible set (PVS) is calculated
is referred to as a <dfn>cell</dfn> or <dfn>portal</dfn>. As an example,
imagine standing in a room in a house. Using only BSP, the game engine
could very quickly determine which rooms you are not facing (as if the
rooms were made of glass and every room were visible from every other
room), and skip drawing them. However, while standing in that room,
there are many other rooms in the house that you likely also cannot see
(as the walls of the rooms are probably not glass and very much opaque).
This is PVS in a nutshell: for that room, the PVS might only be an
adjoining hallway and a closet (assuming that the doors are open). In a
large house with many rooms, in a worst-case scenario (where both the
player is facing the hallway and the closet at the same time), the
engine still has very little to draw as compared to the entire house.
This is discussed in greater detail on [Fabien Sanglard's
blog](http://fabiensanglard.net/doom3/dmap.php).

# Lightmap Calculation

Using the position, color, and type of lights placed in the map editor,
the lightmapper generates a static <dfn>lightmap</dfn> which is
essentially painted over (blended with) the map textures at run-time to
create shadows and areas of light and dark. (Otherwise, the map would be
the same brightness throughout and devoid of shadow). Note that this is
not the extent of the engine's lighting capabilities; additional
(dynamic) lighting is performed in real-time to create effects such as
light generated from muzzle flashes.

### Conventional modeling vs. Radiant