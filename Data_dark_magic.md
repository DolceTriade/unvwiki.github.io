---
title: Data dark magic
permalink: /Data_dark_magic/
---

## About this documentation

This documentation does not provide the easiest instructions to do
things like building a map. For example the NetRadiant level editor
provides a ready-to-use build menu taking care of what's described there
(and details that may not be described there). The `urcheon` tool is
recommended to build Unvanquished assets, and take cares of material
generation, map compilation, image and sound conversion and packaging
including the versioning of the package.

The documentation does not give every details neither all recommended
command line options, but those who are needed even if missing some
other options may result in less optimal results like less good looking
results. For example there is no instructions about the best `q3map2`
options to produce the best-looking lightmaps.

Note: It is assumed the `q3map2` and `daemonmap` commands are used with
`-game unvanquished` option. In the next words, all images will be named
with `.tga` extension because either the tools produce them that way,
either it's easier to do so to make it easier to understand. Sounds may
also be named using the `.wav` extension even if we usually don't use
such format in repositories or in game.

## Packaging files

Files are expected to be stored in DPK archives named like
`map-castle_0.1.dpk`, using
[ZIP](https://en.wikipedia.org/wiki/ZIP_(file_format)) (PKZIP)
compression.

It's recommended to use the `7z` tool with `-tzip -mx=9` options. It's
possible to optimize the compression after that using a Zopfli optimizer
like `advzip` by advancecomp project with `--shrink-insane` option.

## Building a map and producing related files

From `maps/castle.map`, the `q3map2` tool with `-bsp` stage compiles the
map source and produces `maps/castle.bsp`, the `-meta` switch is used at
the same time to merge triangles and optimize the BSP tree (the way the
data is stored).

From `maps/castle.bsp`, the `q3map2` tool with `-vis` stage computes
visibility, the visibility is stored in `maps/castle.bsp` by modifying
it in place.

From `maps/castle.bsp`, the `q3map2` tool with `-light` stage computes
light maps and light grid, the light grid is stored in `maps/castle.bsp`
by modifying it in place. Historically the light map was also stored in
`maps/castle.bsp` by modifying it in place, but the `-meta` switch is
used is to store light maps as `maps/castle/lm_0000.tga`,
`maps/castle/lm_0001.tga`, and with `-deluxe` switch, uneven light map
files are storing lights, and even light map files are storing light
direction.

From `maps/castle.bsp`, the `q3map2` tool with `-minimap` stage computes
minimap and produce `minimaps/castle.tga` and `maps/castle.minimap`, the
first one being the minimap image itself, the second one being a text
file setting some parameters.

From `maps/castle.bsp`, the `daemonmap` tool with `-nav` stage computes
navigation meshes like `maps/chasm-builder.navMesh` and
`maps/chasm-human_bsuit.navMesh`.

The mapper is expected to manually create a levelshot (an image
representing the map) and to store it as `meta/castle/castle.tga`, and
to manually create a file named `meta/castle/castle.arena` which is a
text file containing some metadata about the map (like a displayable
name).

Additionally and optionally, the mapper can add a colorgrade image to
store as `gfx/colorgrade/castle.tga`, the name is not enforced and the
mapper has to edit a specific property in `maps/castle.map` with this
path to enable it (the extension is not needed in the `maps/castle.map`
file), this can be done within NetRadiant level editor using the Entity
Inspector.

    TODO: ability to tweak textures from a .bsp file with esquirel tool.
    TODO: ability to tweak entity lump of a .bsp file with esquirel tool,
          or to update them in a .bsp from a .map using q3map2.
    TODO: ability to generate layouts in game and ship them in dpk.
    TODO: ability to edit navcons in game and ship them in dpk.

## Including a model in a map and building it first

There are two ways to include objects in maps, one is to set them as
`misc_model` entities in the map in NetRadiant level editor, they will
be baked into the map geometry and light maps computed for them, the
other way is to set them as `misc_model_anim` entities in the map in
NetRadiant level editor, they will not be baked to the geometry and
light maps will not be computed for them, the lighting will be computed
from light grid like player models, which is less precise but is
independent of the position.

The `q3map2` map compiler can bake some models in various formats
including ASE, OBJ, MD3 and IQM when using them as `misc_model`
entities. For models set as `misc_model_anim`, the formats are the one
supported by the Dæmon game engine, MD3, MD5Mesh, and IQM.

The ASE, OBJ, MD3, MD5Mesh and IQM models may be produced by some usual
modeling tools and/or using converters.

For models made from modeling tools, the IQM format is recommended.

Models can also be made in NetRadiant level editor as maps, then the
`q3map2` is used to compile and convert map files to the ASE or the OBJ
formats. Both are fine.

From `models/mapmodels/castle/tower.map`, the `q3map2` tool with `-bsp`
stage with `-meta -patchmeta` options compiles the compiles the map
source and produces `models/mapmodels/castle/tower.bsp`.

From `models/mapmodels/castle/tower.bsp`, the `q3map2` tool with
`-convert` stage with `-format ase` option produces
`models/mapmodels/castle/tower.ase`

Alternatively, from `models/mapmodels/castle/tower.bsp`, the `q3map2`
tool with `-convert` stage with `-format obj` option produces
`models/mapmodels/castle/tower.obj`

It's possible to call the `q3map2` tool with `-convert` stage directly
on `models/mapmodels/castle/tower.map` but the produced model will lack
all the optimizations that can be done by the `q3map2` tool with `-bsp`
stage.

## Making materials and textures for maps and models

Materials names to be applied in MAP surfaces must start with
`textures/` prefix since the MAP format strips that prefix one saving
and assumes it on loading.

Historically, all images saved in `textures/` folder are diffuse
materials with light map being computed and applied on, without any
advanced component like normal map, height map, specular or physical
map, or glow map.

Materials are described in text files named like `scripts/castle.shader`
referencing textures stored in `textures/castle_src` folder and setting
some options about the way the material must be rendered. Materials can
set surface parameters (like making a surface translucent, cast shadows,
let projectile pass but not players, make metal clang when walking on
it…) and can set content parameters for the brush made of it (like
forbidding building, making people swim in, or hurting them…).

Multiple materials can be defined in a single `.shader` file.

For example the `textures/castle_custom/brick` material can make use of
`textures/castle_custom_src/brick_d.tga` diffuse texture.

To be usable by the NetRadiant level editor and the `q3map2` map
compiler, the `castle_custom` basename of the
`scripts/castle_custom.shader` file must be listed on a file named
`scripts/shaderlist.txt`. The engine does not need it.

Material names for map models (even those baked in the BSP) or materials
for other purposes do not need to start with the `textures/` prefix.
Same for textures, for example materials and textures for map model
formats may use the same prefix as models, for example a
`models/mapmodels/castle/tower` making use of
`models/mapmodels/castle/tower_d.tga` texture.

The game provides some common materials using `textures/common/` prefix
for common features: preventing to build, clipping player, etc.

Material files can be written by hand, or when possible, be generated by
the `Sloth` tool from existing texture using some name conventions.

It is recommended to generate the material files with the `Sloth` tool
when possible.

It is recommended to not write the file extension of the image in
material files. For example the name can be
`textures/castle_custom_src/brick_d`.

It is recommended to not add a file extension for material names to be
used in the map files, map models, particles, etc. For example the name
can be `textures/castle_custom/brick`.

In some case like when using specific effects like dynamic lightmaps,
the `q3map2` tool may produce a material file named like
`scripts/q3map2_castle.shader`, it is not meant to be listed in
`shaderlist.txt` and not be edited by hand as it will be rewritten on
next compilation.

## Making some graphical effects to be rendered in game

Some graphical effects can be done as materials named like
`gfx/castle/smoke`.

They are stored in material files like `scripts/castle_gfx.shader` but
there is no need to store the base name in `scripts/shaderlist.txt` file
as they are not expected to be used by the `q3map2` tool neither the
NetRadiant level editor.

## Making particle effects to be rendered in game

Particle effects are stored in files named like
`scripts/castle.particle`.

Multiple materials can be defined in a single `.shader` file.

It's recommended to name particle effects with `particles/` prefix.

## Making trail effects to be rendered in game

Trail effect are stored in files named like `scripts/castle.trail`.

Multiple particle effects can be defined in a single `.particle` file.

It's recommended to name particle effects with `trails/` prefix.

## Converting image files for release

It's recommended to store textures as PNG in repositories as widely used
lossless formats are recommended for storage in repositories, if the
best version of a texture is using the JPEG format, it is recommended to
leave it JPEG in repository without any conversion.

It's recommended to optimize PNG (beware that PNG optimizer tools do not
destroy unseen data, like RGB data that can't be seen by fully
transparent alpha channel). The `oxipng` tool without `--alpha` option
is recommended to optimize PNG. It's possible to do a Zopfli
optimization after that using other tools. Prefer using an external
Zopfli optimizer to `oxipng` builtin Zopfli optimizer like
`pngwolf-zopfli` or others, one recommendation is still to be defined.

It's not recommended to use the ImageMagick `convert` tool to convert
from and to TGA format as it is not reliable for this. Other tool to be
determined has to be used instead.

Despite the engine supporting PNG and JPG, it's recommended to convert
images to other formats for being loaded in game.

It is recommended to convert sky boxes into lossy WebP using the `cwebp`
tool.

It is recommended to convert light maps into lossless WebP using the
`cwebp` tool with `-lossless` option.

It is recommended to convert normal maps to normalized DXn CRN format
using the `crunch` tool with the `-dxn -renormalize -rtopmip` options.

It is recommended to ship normal maps and height maps as separate files,
in case height map is stored in normal map alpha channel, it is
recommended to convert such files using the normalized CRN format using
the `crunch` tool with the `-renormalize -rtopmip` options, the `-dxn`
must not be used as it is an optimization trick abusing the alpha
channel and then will not store the height map.

The `crunch` tool must be the Dæmon variant (based on Unity variant).

## Converting sound files for release

It is recommended to store sound files as FLAC in repositories as widely
used lossless formats are recommended for storage in repositories. The
WAV files can be converted to FLAC using the `flac` tool.

It's recommended to name sound effects with `sound/` prefix. For example
a sound file can be named `sound/castle/wind.wav` and stored as
`sound/castle/wind.flac` in a repository.

The engine does not support FLAC anyway.

The engine supports WAV, Ogg Vorbis and Opus audio formats. Ogg Vorbis
sound files must use the `.ogg` file extension and Opus sound files must
use the `.opus` file extension.

It is recommended to convert sound files to Opus except if the best
version available is already using the Ogg Vorbis format.

The FLAC or WAV files can be converted to Opus using the `opusenc` tool
to produce a file named like `sound/castle/wind.opus`.

It's recommended to not convert Ogg Vorbis sound files to Opus and ship
them in Ogg Vorbis format, unmodified.

It is recommended to not write the file extension of the sound path in
map files, for example it can be set as `sound/castle/wind`.