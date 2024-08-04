---
title: Testing Materials
permalink: /Testing/Materials/
---

## Querying loaded data

The command `imagelist` can be used to output a list of all loaded image
files. This command does not support sorting output.

The command `shaderlist` can be used to output a list of all shaders.
`shaderlist` accepts an optional parameter that will filter results by
matching against the shader name, starting from the beginning. An
example of output from `shaderlist` follows:

    ]\shaderlist texture
    -----------------------
    1 3D_S                  SS_OPAQUE           IA : textures/arachnid2/e6dmetal
    1 3D_S                  SS_OPAQUE           IA : textures/arachnid2/dark_metal
    1 3D_S                  SS_OPAQUE           IA : textures/arachnid2/cement_1_gunky
    1 3D_S                  SS_OPAQUE           IA : textures/arachnid2/cement_1_clean

The columns output by `shaderlist` are as follows:

- The number of stages the shader has.
- One of the following:
  - `2D` —
  - `3D_D` —
  - `3D_S` —
  - `ATTN` —

<!-- -->

- One of the following:
  - An empty space.
  - `lighting_DB` —
  - `lighting_DBS` —
  - `reflection_CB` —

<!-- -->

- One of the following:
  - An empty space.
  - `G` —
  - `E` —

<!-- -->

- One of the following:
  - An empty space.
  - `SS_ALMOST_NEAREST` —
  - `SS_BAD` —
  - `SS_BANNER` —
  - `SS_BLEND0` —
  - `SS_BLEND1` —
  - `SS_BLEND2` —
  - `SS_BLEND3` —
  - `SS_BLEND6` —
  - `SS_CLOSE` —
  - `SS_DECAL` —
  - `SS_ENVIRONMENT_FOG` —
  - `SS_ENVIRONMENT_NOFOG` —
  - `SS_FAR` —
  - `SS_FOG` —
  - `SS_MEDIUM` —
  - `SS_NEAREST` —
  - `SS_OPAQUE` —
  - `SS_PORTAL` —
  - `SS_POST_PROCESS` —
  - `SS_SEE_THROUGH` —
  - `SS_UNDERWATER` —
  - `SS_WATER` —

<!-- -->

- One of the following:
  - An empty space.
  - `IA` —

<!-- -->

- The shader name. The text "`(DEFAULTED)`" will be appended to the
  shader name if it cannot be found.

[Category:Testing](Category:Testing "wikilink")
[Category:Mapping](Category:Mapping "wikilink")