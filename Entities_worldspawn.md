---
title: Entities worldspawn
permalink: /Entities/worldspawn/
---

## worldspawn (0 0 0) ?

Used for game-world global options. Every map should have exactly one.

message: Text to print during connection process. Used for the name of level.
music: path/name of looping .wav file used for level's music (eg. music/sonic5.wav).
gravity: level gravity \[g_gravity (800)\]

<!-- -->

humanBuildPoints: maximum amount of power the humans can use. \[g_humanBuildPoints\]
alienBuildPoints: maximum amount of sentience available to the overmind. \[g_alienBuildPoints\]

<!-- -->

humanMaxStage: The highest stage the humans are allowed to use (0/1/2). \[g_alienMaxStage (2)\]
alienMaxStage: The highest stage the aliens are allowed to use (0/1/2). \[g_humanMaxStage (2)\]

<!-- -->

disabledEquipment: A comma delimited list of human weapons or upgrades to disable for this map. \[g_disabledEquipment ()\]
disabledClasses: A comma delimited list of alien classes to disable for this map. \[g_disabledClasses ()\]
disabledBuildables: A comma delimited list of buildables to disable for this map. \[g_disabledBuildables ()\]

### Q3MAP2 KEYS

_ambient OR ambient: Adds a constant value to overall lighting. Use is not recommended. Ambient light will have a tendency to flatten out variations in light and shade.
_color: RGB value for ambient light color (default is 0 0 0).
gridsize: Dynamic Light Granularity - granularity of the lightgrid created by q3map. Value is three integers separated by spaces, representing number of units between grid points in X Y Z. Default gridsize value is 128 128 256. Use larger powers of 2 to reduce BSP size and compile time on very large maps.
_minlight: Minimum light value, levelwide. Uses the _color key to set color. Does not add unlike ambient.
_minvertexlight: Minimum vertex lighting, levelwide.
_mingridlight: Minimum lightgrid (dynamic entity lighting) levelwide.
_noshadersun: Ignore q3map_sun/sun directives in sky shaders and ONLY use entity sun lights.
_ls OR _lightmapscale: Lightmap Scale - Floating point value scaling the resolution of lightmaps on brushes/patches in the world. Can be overridden in func_group (or other entities) (default 1.0).
_keeplights: Keep light entities in the BSP. Normally stripped out by the BSP process and read from the .map file by the lighting phase.

<!-- -->

_celshader: Sets the cel shader used for this geometry. Note: omit the "textures/" prefix. Overridable in entities.
_foghull: Shader to use for "fog hull." Foghull shader should be a sky shader. Omit the "textures/" prefix.
_cs OR _castshadows: Allows per-entity control over shadow casting. Defaults to 0 on entities, 1 on world. 0 = no shadow casting. 1 = cast shadows on world. \> 1 = cast shadows on entities with _rs (or _receiveshadows) with the corresponding value, AND world. Negative values imply same, but DO NOT cast shadows on world.
_rs OR _receiveshadows: Allows per-entity control over shadow reception. Defaults to 1 on everything (world shadows). 0 = receives NO shadows. \> 1 = receive shadows only from corresponding keyed entities (see above) and world. \< 1 = receive shadows ONLY from corresponding keyed entities.

<!-- -->

_blocksize: BSP Block Size - q3map always splits the BSP tree along the planes X=_blocksize\*n and Y=_blocksize\*n. Default _blocksize value is 1024. Increase the blocksize using larger powers of 2 to reduce compile times on very large maps with a low structural brush density.
_farplanedist: Limit on how many units the vis phase of compilation can see. Used in combination with level-wide fog, it can help reduce r_speeds on large, open maps.

### Q3MAP2 TERRAIN KEYS

_indexmap: Path/name for the art file used to guide the mapping of textures on the terrain surface.
_layers: Integer value is the number unique root shaders that will be use on the terrain.
_shader: Path to the metashader used to assign textures to the terrain entity. Note: Omit the "textures/" prefix.

## Reserved or Currently unused

humanStage2Threshold: The number of kills the humans must aquire to advance to stage 2. Defaults to \[g_humanStage2Threshold\].
humanStage3Threshold: The number of kills the humans must aquire to advance to stage 3. Defaults to \[g_humanStage3Threshold\].
alienStage2Threshold: The number of kills the aliens must aquire to advance to stage 2. Defaults to \[g_alienStage2Threshold\].
alienStage3Threshold: The number of kills the aliens must aquire to advance to stage 3. Defaults to \[g_alienStage3Threshold\].

[Category:Mapping](Category:Mapping "wikilink")