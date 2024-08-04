---
title: Entities Lights
permalink: /Entities/Lights/
---

Most light entities are interpreted by the map compiler and stripped
from the resulting BSP. If you pass `-keeplights` to the map compiler,
it won't strip them. In that case the Renderer might use them for
dynamic lights, but the game (qvm) will free them instantly after a
spawn again.

## light (.65 .65 1) (-8 -8 -8) (8 8 8) LINEAR NOANGLE UNUSED1 UNUSED2 NOGRIDLIGHT

Non-displayed point light source. The -pointscale and -scale arguments
to Q3Map2 affect the brightness of these lights. The -skyscale argument
affects brightness of entity sun lights. Especially a target_position is
well suited for targeting.

### Q3MAP2 KEYS

target: Lights pointed at a target will be spotlights. This will only take targetname and not the multi-targetnames into account
radius: overrides the default 64 unit radius of a spotlight at the target point.
_light OR light: overrides the default 300 intensity.
_color: weighted RGB value of light color (default white - 1.0 1.0 1.0).
_sun: Set this key to 1 on a spotlight to make an infinite sun light.
fade: Fades light attenuation. Only affects linear lights.
scale: Scales light attentation, from SOF2/JK2. Scales the "light" value.

### SPAWNFLAGS

LINEAR: Use a linear falloff. Default is inverse distance squared (more realistic).
NOANGLE: Ignore angle attenuation.
NOGRIDLIGHT: Do not affect the lightgrid (dynamic entity lighting).

## lightJunior (0 0.7 0.3) (-6 -6 -6) (6 6 6) LINEAR NOANGLE UNUSED1 UNUSED2 NOGRIDLIGHT

Non-displayed point light source THAT ONLY AFFECTS ENTITIES (lightgrid).
The -pointscale and -scale arguments to Q3Map2 affect the brightness of
these lights. The -skyscale argument affects brightness of entity sun
lights. Especially a target_position is well suited for targeting.

### Q3MAP2 KEYS

target: Lights pointed at a target will be spotlights. This will only take targetname and not the multi-targetnames into account
radius: overrides the default 64 unit radius of a spotlight at the target point.
_light OR light: overrides the default 300 intensity.
_color: weighted RGB value of light color (default white - 1.0 1.0 1.0).
_sun: Set this key to 1 on a spotlight to make an infinite sun light.
fade: Fades light attenuation. Only affects linear lights.
scale: Scales light attentation, from SOF2/JK2. Scales the "light" value.

### SPAWNFLAGS

LINEAR: Use a linear falloff. Default is inverse distance squared (more realistic).
NOANGLE: Ignore angle attenuation.
NOGRIDLIGHT: Do not affect the lightgrid (dynamic entity lighting). Setting this spawnflag will disable this light entirely.

[Category:Mapping](Category:Mapping "wikilink")