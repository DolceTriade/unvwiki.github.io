---
title: Formats DPK
permalink: /Formats/DPK/
---

## About the DPK name

*DPK* stands for *“Dæmon PacKage”*, the DPK VFS is a *PacKage*-based VFS
leveraging *Dependency* mechanism.

## DPK format specification

The DPK format extends the legacy PK3 format with dependency mechanism
and versionning and was implemented for the need of the [Unvanquished
game](https://unvanquished.net/). Like the PK3 VFS, the DPK VFS allows
to extend and override an existing file system using packages, see the
[Filesystem](Filesystem "wikilink") page to see how it works. The is the
reference implementation, it has been introduced under this name in
Unvanquished 0.51.0 release.

There is two DPK formats: archive and directory format.

- Archive format is for distribution (commonly named *DPK*), this format
  is meant to be easily shareable over the network and auto-downloadable
  by game clients;


The archive format uses the PKZIP container (the well-known *zip*
format) with a *.dpk* extension.

- Directory format is for editing/testing (commonly named *DPKDIR*);


The directory format is a simple plain directory with a *.dpkdir*
extension.

### Package naming

Format: *<package-name>_<version-string>.<extension>*

- package-name: name of the package, some names are prefixed

:\* mandatory prefix for map packages: *“map-”* (the engine will not
find neither load the map otherwise)

:\* recommended prefix for texture packages: *"tex-”*

:\* recommended prefix for various resource packages (like a package
providing both sounds effects, textures, models and animation for a
given player model) : *"res-”*

:\* forbidden characters: underscore, dot *\[_.\]*

- version: version of the package, follows [dpkg's version comparison
  priority](https://salsa.debian.org/dpkg-team/dpkg/-/blob/main/lib/dpkg/version.c),
  see [Packaging version
  guidelines](Packaging_version_guidelines "wikilink") for Unvanquished
  specificities.

:\* characters allowed: alphanumeric plus hyphen and tilde
*\[a-zA-Z0-9~-\]*

- extension: *“dpk”* for archive, *“dpkdir”* for directory

Examples:

- *unvanquished_0.51.0.dpk*
- *map-parpax_0.5d-viech.dpk*
- *tex-vega_src.dpkdir*
- *res-players_src.dpkdir*

### Package layout

Package archive or directory can contain a *DEPS* file on its root
directory containing a list of other package it depends on.

Each package reproduces the file system tree from his root.

### DEPS file format

- One package name per line, optional explicit version separated from
  package name using a whitespace;
- Dependencies are loaded giving priority to first ones if multiple
  package provides different files under the same name.

Example:

    tex-space
    tex-pk02 1.0
    tex-vega 0.4b

Loading a package providing this *DEPS* file will trigger the game
engine to also load the *tex-space* package (the most recent version
found), and to load the 1.0 version of the *tex-pk02* package and the
0.4b version of the tex-vega package.

## Software compatibility

Software that support DPK format and have first class Unvanquished
support:

- [Dæmon](Engine "wikilink") game engine:
  full dpk/dpkdir support with dependency and version handling,
  support in master branch;
- [NetRadiant](Tools_NetRadiant "wikilink") level editor:
  full dpk/dpkdir support with dependency and version handling,
  support in master branch;
- [q3map2](Tools_q3map2 "wikilink") map compiler (NetRadiant tree):
  basic dpk/dkdir support, loads all dpk/dpkdir it finds,
  support in master branch;
- [Chameleon](Tools_Chameleon "wikilink") texture replacement editor:
  basic dpk/dpkdir support, loads all dpk/dpkdir it finds,
  support in master branch;
- [Urcheon](Tools_Urcheon "wikilink") package build tool:
  basic dpkdir support, loads all dpkdir it finds,
  support in master branch;
- [XQF](XQF "wikilink") game server browser:
  basic dpk support, loads all dpk it finds,
  support in master branch.

Other software that are known to support DPK format and have working
Unvanquished support:

- [GtkRadiant](Tools_GtkRadiant "wikilink") level editor:
  basic dpk/dkdir support in master branch, loads all dpk/dpkdir it
  finds,
  support in master branch,
  prefer using NetRadiant if possible and if NetRadiant is not possible
  prefer q3map2 from NetRadiant tree;
- [q3map2](Tools_q3map2 "wikilink") map compiler (GtkRadiant tree):
  basic dpk/dkdir support, loads all dpk/dpkdir it finds,
  support in master branch,
  not recommended for Dæmon mapping due to feature lacking.

Other software that are known to support DPK format but have not working
Unvanquished support:

- [DarkRadiant](tools_DarkRadiant "wikilink") level editor: basic
  dpk/dpkdir support, loads all dpk/dpkdir it finds,
  support in standard releases (just add "dpk" to game file),
  not yet usable for Dæmon/Unvanquished mapping due to some Q3 map
  parsing issues.

## Merging several DPK

To combine all packages together, at a Bash shell:

`$ cd `[<var>`data directory`</var>](Game_locations "wikilink")`/pkg; mkdir tmp; for pk3 in pak{{0..9},A}.pk3; do unzip -o $pk3 -d tmp; done`

(If there are additional `pak*` files (e.g., `pakB.pk3`), edit the
pattern accordingly (e.g., to `pak``.pk3`.)

This will place the cumulative contents (i.e., as the engine would see
them) of all the `pak*.pk3` archives into a new `tmp/` directory in your
data directory.

[Category:Formats](Category:Formats "wikilink")
[Category:Mapping](Category:Mapping "wikilink")