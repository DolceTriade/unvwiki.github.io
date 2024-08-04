---
title: Entities misc model
permalink: /Entities/misc_model/
---

## misc_model (1 .5 .25) (-16 -16 -16) (16 16 16) CASTSHADOW AUtOCLIP FORCEMETA

Generic placeholder for inserting MD3 models in game. Requires
compilation of map geometry to be added to level. If the map is compiled
with Q3Map2, then ASE, 3DS, OBJ and other model formats are supported.

### Q3MAP2 KEYS

angle: direction in which model will be oriented.
model: path/name of model to use (eg: models/mapobjects/teleporter/teleporter.md3).
angles: Individual control of PITCH, YAW, and ROLL (default 0 0 0).
modelscale: Floating-point value used to scale a model up or down (default 1.0).
modelscale_vec: Floating-point vector used to scale a model's axes individually (default 1.0 1.0 1.0).
_remap: Used to remap textures/shaders in the model. To remap all shaders to a given shader, use "\*;models/mymodel/mytexture". To remap a specific shader, use "models/mymodel/old;models/mymodel/new".
target: Used to attach the misc_model to a brush entity, where its "targetname" key is the same value.
_lightmapscale: Floating point value scaling the resolution of lightmaps on this model (if model is using lightmapped shaders) (default 1.0).
_cs OR _castshadows: Allows per-entity control over shadow casting. Defaults to 0 on entities, 1 on world. 0 = no shadow casting. 1 = cast shadows on world. \> 1 = cast shadows on entities with _rs (or _receiveshadows) with the corresponding value, AND world. Negative values imply same, but DO NOT cast shadows on world.
_rs OR _receiveshadows: Allows per-entity control over shadow reception. Defaults to 1 on everything (world shadows). 0 = receives NO shadows. \> 1 = receive shadows only from corresponding keyed entities (see above) and world. \< 1 = receive shadows ONLY from corresponding keyed entities.
_celshader: Sets the cel shader used for this geometry. Note: omit the "textures/" prefix.

### SPAWNFLAGS

CASTSHADOW: Toggles the model casting shadows on the map surfaces.
AUTOCLIP: Sets the autoclipping spawnflag, automatically assigning q3map_clipmodel to any shaders used by the model. Use of Q3Map2 autoclipping for models is only recommended for large models with relatively few triangles in their mesh (i.e. terrain). The Q3Map2 autoclipping algorithm is a bit of a hack, and can hurt in-game performance (as well as produce erroneous clipping results) when used on small, dense models.
FORCEMETA: Sets the forcemeta spawnflag, automatically adding q3map_forcemeta to any shaders used by the model (which, in turn, allows the model to become lightmapped). This, effectively, is the "lightmapped model" spawnflag.