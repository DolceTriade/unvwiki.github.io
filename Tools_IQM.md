---
title: Tools IQM
permalink: /Tools/IQM/
---

Here are some known tools supporting IQM/IQE formats (or with
work-in-progress support).

## Frequently asked questions

- IQE to IQM conversion: see [iqmtool](#iqmtool "wikilink");
- IQM to IQE conversion: see [asstools](#asstools "wikilink");
- Blender Exporter: see [IQM Development
  Kit](#IQM_Development_Kit "wikilink");
- Blender Importer: see [asstools](#asstools "wikilink");
- Viewer: see [IqeBrowser](#IqeBrowser "wikilink") and
  [Noesis](#Noesis "wikilink");
- Converter to many formats: see [Noesis](#Noesis "wikilink");
- Game level editor and map compiler recommended for Unvanquished: see
  [NetRadiant](#NetRadiant "wikilink") and [Q3map2](#Q3map3 "wikilink")
  from NetRadiant.

## IQM tools

### iqmtool

**Repository:** <https://svn.code.sf.net/p/fteqw/code/trunk/iqm>

### asstools

Some free open source tools, including a Blender import plugin (but it
has to be ported to latest Blender version).

Also provides a `iqm_to_iqe.py` tool that can convert `.iqm` files back
to `.iqe` ones.

**Repository:** <https://github.com/ccxvii/asstools>

### IQM Development Kit

Original Lee Salzman's free open source reference project for IQM. It
provides a Blender export plugin, and a tool to convert some formats to
IQM (including Doom 3's md5mesh/anim).

For the command line tool prefer the FTEQW's `iqmtool` one (see
[iqmtool](#iqmtool "wikilink")) if you're contributing to Unvanquished
(it's a fork with more features we rely on).

**Website:** <http://sauerbraten.org/iqm/>

### IqeBrowser

A free open source graphical viewer and converter. Unfortunately only
built for Windows (and there are some Windowsism in code), but works
well on Wine.

**Download page:**
<https://www.moddb.com/mods/r-reinhard/addons/iqebrowser-v217>

**Forum thread:**
<https://forums.unvanquished.net/viewtopic.php?f=8&t=2106>

### Noesis

A free (gratis) graphical viewer and converter. Unfortunately only built
for Windows, but works well on Wine.

**Download page:**
<http://richwhitehouse.com/index.php?content=inc_projects.php>

## Tools with IQM support

### NetRadiant

NetRadiant supports `.iqm` model rendering in the editor thanks to IQM
implementation in picomodel library and the provided
[Q3map2](Tools_Q3map2 "wikilink") map compiler can now bake `.iqm` files
(see below).

**Website:** <https://netradiant.gitlab.io>

### Q3map2

The q3map2 map compiler from upstream NetRadiant can now bake `.iqm`
files.

**Website:** <https://netradiant.gitlab.io>

### GtkRadiant

Another level editor initially purposed for Quake 3 mapping that is also
usable for Unvanquished mapping (see [Level
editors](Tools_Level_editors "wikilink")), it now supports rendering IQM
models thanks to IQM implementation in picomodel library.

The q3map2 map compiler from GtkRadiant can now bake `.iqm` files but is
not recommended for Unvanquished mapping (it does not support some other
features we want). If you map with GtkRadiant editor, please compile
your maps with NetRadiant's q3map2.

**Website:** <https://icculus.org/gtkradiant/>

### DarkRadiant

Another level editor initially purposed for Doom 3 mapping that is also
usable for Unvanquished mapping (see [Level
editors](Tools_Level_editors "wikilink")), it now supports rendering IQM
models thanks to IQM implementation in picomodel library. The integrated
animation viewer does not support IQM animation though.

**Website:** <https://www.darkradiant.net>

## Tools with work in progress IQM support

### Maverick Model 3D

A free open source graphical viewer, with IQM format being work in
progress (may not be already usable or even available in releases).

It's a fork of Misfit Model 3D, maintained by ZTM.

**Website:** <https://clover.moe/mm3d/>

[Category:Tools](Category:Tools "wikilink")
[Category:IQM](Category:IQM "wikilink")