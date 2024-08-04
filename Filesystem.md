---
title: Filesystem
permalink: /Filesystem/
---

Unvanquished stores its resources (maps, sounds, textures, models etc)
in *packages*. To be able to use your own resources in the game you must
put them in a package.

Note: The Unvanquished filesystem rules differ from Tremulous and Quake.

# Overview

A package is simply a zip-file or a folder containing resources. When a
package is loaded its contents are extracted into a virtual filesystem
(analogous to a hidden folder). If two packages have the same file, the
file that was first extracted always wins out -- files cannot be
overwritten once they are in the filesystem (this differs greatly to the
traditional quake behavior).

The game only loads packages as it needs them:

- Main *unvanquished* package (containing base game resources) is always
  loaded first.
- Map packages as they are necessary
- Any packages that the above say they depend on (eg texture-packs)

Other packages can be forced to load using fs_extrapaks (detailed
below).

Every package has a version number. When a package is loaded the latest
version is used. For example:

` tex-awesometextures_2016-04-25.dpkdir`

In this case an enterprising author made their package version an ISO
date (YYYY-MM-DD) to ensure that the latest version always has the
'largest' version number. There are [recommended versioning
guidelines](Packaging_Version_Guidelines "wikilink") that go into more
detail. To load multiple version of the same package, the one with the
'largest' version number must list the ones with 'smaller' version
number as dependencies in DEPS file.

There are two ways packages can be stored: as dpks or dpkdirs. Packages
ending in .dpkdir are plain folders whilst .dpk's are zip-compressed
files. Generally it's easier to work with a dpkdir folder and then make
a compressed copy only when needed to send over the web.

## Locations

Packages can be stored in the 'pkg' folder found in two places: the game
installation path ("libpath") or the user's own personal path
("homepath").

<span id="Pakpaths"></span>

### Pak search paths

The directories in which Daemon searches for packages, known as
**pakpaths**, are:

- <homepath>`/pkg`
- <libpath>`/pkg`
- Any additional locations added by the `-pakpath` command line switch

## Filesystem priority

Once a file is in the filesystem, nothing can change it or replace it.
If two packages have the same file then the first one to be loaded
becomes dominant. The moment a package is loaded, if it contains a DEPS
file, its dependencies are loaded recursively in the order of the DEPS
file.

The names of packages to load come from:

1.  fs_extrapaks if set: each pak in the space-separated values is
    loaded starting from the left.
2.  main package configured by `fs_basepak` (default: "unvanquished")
3.  map, as needed.

Dependencies are loaded immediately after their parent package, in the
order specified in the DEPS file. Recursive dependencies are loaded in
depth-first order.

Whole-game modifications can still use the main unvanquished package by
listing it as one of their dependencies. Otherwise fs_extrapaks can just
be used.

# Packaging Details

See for more details.

## Naming

Map package names *must* start with *map-* prefix or the engine will not
list and not load them. The package name after the *map-* prefix must be
the bsp base name, for example *map-station15_1.0.dpk* contains the
*maps/station15.bsp* file. As best practice, it's recommended texture
package names start with the *tex-* prefix. It's recommended packages
shipping mixed resources (map models, sounds, gfx…) are named using a
*res-* prefix. More similar prefixes would be defined in the future if
needed.

Packages have three parts to their filename:

- the package basename (eg map-nano)
- the version (eg 2)
- the extension (eg .dpk)

In this case our filename would be *map-nano_2.dpk*

Rules:

- Underscores must be used to separate the name from the version, but
  may not be used anywhere else
- Authors intending to release their work should follow the [Packaging
  Version Guidelines](Packaging_Version_Guidelines "wikilink")

Sometimes a fourth section (a
[checksum](https://en.wikipedia.org/wiki/checksum)) is included when
auto-downloading maps. This should never be added manually.

## Types

- **.dpkdir** is for folders
- **.dpk** is for zip-compressed packages

To convert from a dpkdir to a dpk:

1.  Compress the *contents* of a dpkdir (not the folder itself) into a
    zip-file
2.  Rename this zip file so that it ends with .dpk

# Filesystem layout

Every package is 'extracted' into the same root folder in the
filesystem.

It is recommended you follow the traditional folder-structure for your
packages. When there is a chance files from another package may have
similiar names, you should make a subfolder with your packages name to
avoid a clash. Examples of this are below.

## Recommended folder structure

| Folder       | Description and notes                                                                                                               | Example                                                                        |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------|
| /about       | Info and licensing about your package.                                                                                              | /about/map-parpax.txt                                                          |
| /textures    | .crn texture files                                                                                                                  | /textures/parpax_evillair/                                                     |
| /sound       | .opus sound files                                                                                                                   | /sound/parpax                                                                  |
| /scripts     | .shader, .particle files                                                                                                            | /scripts/parpax_custom.shader /scripts/parpax.particle                         |
| /minimaps    | .crn picture, .minimap description file                                                                                             | /minimaps/parpax_upper.crn /minimaps/parpax_lower.crn /minimaps/parpax.minimap |
| /map         | .map, .bsp, .navMesh (for bots)                                                                                                     | /map/parpax.bsp                                                                |
| /meta        | "Loading screen" picture of a map level (.jpg so it can be use by third party tools), .arena metadata file containing the real name | /meta/parpax/parpax.jpg /meta/parpax/parpax.arena                              |
| /gfx         | Colorgrade (lossless)                                                                                                               | /gfx/parpax/colorgrading.png                                                   |
| /DEPS (file) | Depedencies file. See next section.                                                                                                 | /DEPS                                                                          |
|              |                                                                                                                                     |                                                                                |

Example of meta in loading screen:
![<File:Downloading_map_compiling_GLSL_shaders.png>](Downloading_map_compiling_GLSL_shaders.png "File:Downloading_map_compiling_GLSL_shaders.png")

## DEPS file

A DEPS file in the root of a package tells the game what dependencies
are required for this package. Dependant packages are loaded after the
current package, so if any files clash then the dependencies 'lose out'.

Example contents of a DEPS file (from map-parpax_2.5.1.dpk):

`res-ambient`
`tex-common`
`tex-ex`
`tex-exm`
`tex-pk01`
`tex-pk02`
`tex-space`
`tex-trak5`

# Guides

## Creating your own package

Find your user's package directory

![[`File:Dir`](File:Dir)` homepkg.png`](Dir_homepkg.png "File:Dir homepkg.png")

Create a dpkdir folder

![[`File:Dir_homepkg_newfolder.png`](File:Dir_homepkg_newfolder.png)](Dir_homepkg_newfolder.png "File:Dir_homepkg_newfolder.png")

Place inside the files you want to use. Make sure you follow the
filesystem organisation guidelines, or [kangz](User:Kangz "wikilink")
will eat you.

![[`File:Dir`](File:Dir)` inpackage.png`](Dir_inpackage.png "File:Dir inpackage.png")

If your package is a map, you can */devmap mapname* in the
[console](console "wikilink") to load it. Otherwise you may want to
force it to be loaded with *fs_extrapaks*.

`$ unvanquished -set fs_extrapaks tutorialexample`

## Using the latest resources from git

See [Running Unvanquished from
Git](Tutorials_Running_Unvanquished_from_Git "wikilink").