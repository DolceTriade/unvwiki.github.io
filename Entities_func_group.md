---
title: Entities func group
permalink: /Entities/func_group/
---

## func_group (0 .5 .8) ?

This is not an entity as such. It is strictly an editor utility to group
world brushes and patches together for convenience (selecting, moving,
copying, etc). You cannot group entities with this. Groups are turned
into whole brushes by the utilities.

### Q3MAP2 KEYS

_lightmapscale: Floating point value scaling the resolution of lightmaps on brushes/patches in this entity (default 1.0).
_cs OR _castshadows: Allows per-entity control over shadow casting. Defaults to 0 on entities, 1 on world. 0 = no shadow casting. 1 = cast shadows on world. \> 1 = cast shadows on entities with _rs (or _receiveshadows) with the corresponding value, AND world. Negative values imply same, but DO NOT cast shadows on world.
_rs OR _receiveshadows: Allows per-entity control over shadow reception. Defaults to 1 on everything (world shadows). 0 = receives NO shadows. \> 1 = receive shadows only from corresponding keyed entities (see above) and world. \< 1 = receive shadows ONLY from corresponding keyed entities.
_celshader: Sets the cel shader used for this geometry. Note: omit the "textures/" prefix.

### Q3MAP2 TERRAIN KEYS

_indexmap: Path/name for the art file used to guide the mapping of textures on the terrain surface.
_layers: Integer value is the number unique root shaders that will be use on the terrain.
_shader: Path to the metashader used to assign textures to the terrain entity. Note: Omit the "textures/" prefix.

### NOTES

The TAB key can be used to flip through the component pieces of a
selected func_group entity, isolating individual components. To make a
func_group into a terrain entity, refer to the Terrain Construction
documentation.