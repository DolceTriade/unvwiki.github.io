---
title: Formats IQM
permalink: /Formats/IQM/
---

## Tools

See [Tools/IQM](Tools_IQM "wikilink").

## Inter-Quake Model

### Bone-based model and skeletal animation format

The [Inter-Quake Model](http://sauerbraten.org/iqm/) (IQM) format was
developed by Lee Salzman (aka eihrul) as a more modern alternative to
the formats popularly used in the open-source community prior to its
introduction.

The `.iqm` files are binary files.

The `.iqe` files are text counterpart. Unvanquished stores `.iqe` files
in asset source repositories and ships `.iqm` files in `.dpk` archives.

Both IQM and IQE files can embed models with bones and skeletal
animations.

### Adoption

IQM format is popular in free open source games, mods and free open
source game engines like Cube 2: Sauerbraten, Red Eclipse/Blue Nebula,
Xonotic (DarkPlaces), Alien Arena, Warsow/Warfork (QFusion),
Unvanquished (Dæmon), Ya3dag, FTEQW, ioquake3, and others. It became a
de-facto standard for such free open source gaming projects.

IQM format is fully supported in Unvanquished workflow : in engine,
asset build tools, level editor, map compiler, etc.

### Advantages of IQM over MD5

MD5 format (`.md5mesh`/`.md5anim`) was the skeletal model and animation
format used by Doom 3, which is also supported by the [Dæmon
Engine](Engine "wikilink") alongside IQM (MD5 was implemented first in
XreaL, then IQM was implemented in Dæmon).

We recommend using IQM when possible. Advantages of IQM over MD5 are:

- Triangle adjacency data;
- Non-uniform joint scaling;
- Variable vertex attributes:
  - Position (equivalent to MD2 and MD3 style of animation);
  - Texture coordinates;
  - Normals;
  - Tangents;
  - Weights;
  - Colors;
- Animation and model files may be combined (if desired);
- A binary (“compiled”) format is available (no text parsing at run
  time).

### Specification

- IQM Homepage:
  <http://sauerbraten.org/iqm/>
- IQM Binary format specification:
  <http://sauerbraten.org/iqm/iqm.txt>
- IQE Plain-text format specification:
  <http://sauerbraten.org/iqm/iqe.txt>
- IQM development kit and reference implementation by Lee Salzman:
  <https://github.com/lsalzman/iqm>

### Recommended tool

The recommended tool to convert models to IQM format is
[Iqmtool](Tools_Iqmtool "wikilink").

### Implementation

Dæmon developer gimhael [submitted a
patch](https://bugzilla.icculus.org/attachment.cgi?id=2673&action=diff)
in 2011 to the [ioquake3 bug
tracker](https://bugzilla.icculus.org/show_bug.cgi?id=4965). Later in
2013, gimhael also
[implemented](https://github.com/DaemonEngine/Daemon/commit/8b9a672024e97a793cea9f661c44a7b096936537)
IQM in as well.

[Category:Formats](Category:Formats "wikilink")
[Category:IQM](Category:IQM "wikilink")