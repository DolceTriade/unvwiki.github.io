---
title: Formats BSP
permalink: /Formats/BSP/
---

The file is compiled to a file file using the map compiler.

The BSP format is engine specific.

Since id Tech engines weren't designed to be repurposable without
forking, almost every idTech-based games shipped their own specific
engine fork and may have implemented incompatible variants of BSP (it
exists dozens if not hundreds of variants of BSP format).

The BSP file is a binary format. The supports the IBSP46 and IBSP47
formats which are Quake 3 and Wolfenstein:Enemy Territory formats (they
are basically the same with a different header).

A BSP file is named this way because it stores the BSP tree (see [Binary
space
partitioning](https://en.wikipedia.org/wiki/Binary_space_partitioning)),
but in fact the BSP file stores more things than that. It also stores
lightgrid, entities, it may store lightmaps (we recommend to use
external ones though), and many other things.

A BSP file is usually made of multiple parts named <dfn>lump</dfn> which
are stored one after one with an array storing their address at the
beginning of the file. The format is very primitive and is hard to
extend as it does not tell how many lumps there are or what kind of data
each lump stores, the developer has to know it according to the version
number, praying that no one reused the same version for another format.

In Dæmon ecosystem and idTech one the BSP file is never distributed
alone, it is shipped within a package, a one for Dæmon based games,
other idTech games may ship them in packages like PK3 (Quake 3
derivatives) or PK4 (Doom 3 derivatives). For a DPK containing a BSP we
usually talk about a “*map pak*”.

## Documentation about the BSP format

### Unofficial Quake 3 Map Specs

by Kekoa “Mr Alligator” Proudfoot.

Despite its name it's about format, not format.

URL: <https://www.mralligator.com/q3/>

Mirrors:

- <http://arrrgh.fr/mapping/unofficial_quake_3_map_specs.html>
- <https://dl.grangerhub.org/files/mirrors/arrrgh.fr/unofficial_quake_3_map_specs.html>

### Rendering Quake 3 Maps

by Morgan McGuire, it is intended to be a sequel to *Unofficial Quake 3
Map Specs*.

Despite its name it's about format, not format.

Mirrors:

- <http://arrrgh.fr/mapping/unofficial_rendering_quake_3_map.html>
- <https://dl.grangerhub.org/files/mirrors/arrrgh.fr/unofficial_rendering_quake_3_map.html>

### Unofficial Quake 3 BSP Format

by Ben “Digiben” Humphrey.

Mirrors:

- <http://arrrgh.fr/mapping/unofficial_quake_3_bsp_format.html>
- <https://dl.grangerhub.org/files/mirrors/arrrgh.fr/unofficial_quake_3_bsp_format.html>

## Related documentation

### Triangle Meshes in Q3

by Kekoa Proudfoot, companion to *Unofficial Quake 3 Map Specs*.

URL: <https://www.mralligator.com/q3/trimesh/>

[Category:Formats](Category:Formats "wikilink")
[Category:Mapping](Category:Mapping "wikilink")