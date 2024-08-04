---
title: Formats Material
permalink: /Formats/Material/
---

Materials were named *shaders* at Quake 3 time, they must not be
confused with *[GLSL](Formats_GLSL "wikilink") shaders*.

Material format is engine specific (mods don't modify it).

See also [Particle](Formats_Particle "wikilink") and
[Trail](Formats_Trail "wikilink").

## Supported material formats and keywords

The supports:

- Quake 3 materials in files named like `scripts/`<basename>`.shader`
  with Quake 3 material syntax and keywords (if it's not 100%
  compatible, it's a bug, please report!);
- Some Doom 3 material keywords like `normalMap` and others, but the can
  stage them too (it was a regression from Doom 3), files named like
  `materials/`<basename>`.mtr` are not supported.
- Some Darkplaces keywords like `dpoffsetmapping` or `dpreflectcube`,
  features like implicit image sidecar loading and compatibility with
  Darkplaces blending limitations when enabling `r_dpMaterial` and
  `r_dpBlend`.
- Specific features like physical mapping, reflect mapping and others,
  with the ability to stage them, and other keywords like `normalFormat`
  to support multiple formats for normal maps.

## Legacy guides

The [Q3 shader
manual](https://icculus.org/gtkradiant/documentation/Q3AShader_Manual/)
is useful to grasp the legacy keywords and syntax, not all things
described here are optimal in Dæmon (we sometime improved Dæmon to offer
easier syntax), but this is useful to understand legacy shaders, and
everything from this manual should be supported in Dæmon (otherwise we
want to fix it).

The [Q3map shader
manual](http://q3map2.robotrenegade.com/docs/shader_manual/) is useful
to get the knowledge about options specific to map compilation, namely
the -prefixed options that are prrocessed by the Q3map2 map compiler.

The [XReal shader
manual](http://tremap.xtr3m.net/__Games/Xreal/Manual_Shader_1/ShaderManual.htm)
may also be a useful reference, keeping in mind some things differs in
Dæmon, some features may not be implemented or in better ways, for
example the way to set a height map as documented in this manual is not
supported and a far easier option is offered in Dæmon (see the keyword).

## Texture creation

See [Image](Formats_Image "wikilink") for details on texture formats and
packing.

## Texture naming conventions and material keywords

## Dept, doubt and shortcoming

### Preview image

While optional to be rendered in game, a material should feature a
preview image to be rendered in the level editor. It can be different
from the diffuse map, but if the preview does not have to be different,
just reuse the diffuse map.

The first reason why it exists is that the actual material image to be
rendered in game may uses a format that is unknown to the level editor
or the map compiler.

### Normal map

Quake 3-like `.shader` material files assume `X -Y Z` like DirectX
because XreaL mimicked DOOM3 that followed that standard, it's possible
to use `X Y Z` (OpenGL-like) with the keyword `normalFormat X Y Z` (or
any unconventional variant). The `normalScale` keyword can also be used
to scale the normal map components this way: `normalScale .3 .4 2`.

### Gloss map

Maybe the engine supports Gloss map in alpha channel of specular maps.
Some of our model textures provide additional data in alpha channel of
specular maps, and the renderer does some computation with it. We should
investigate what's this computation is for. Some people call gloss map
the specular map, but some people seems to design two different things
with those two different names. The [About page of
Unvanquished](https://unvanquished.net/about/) says: “*Support for glow,
gloss, specular, and physical mapping*”, so maybe the gloss map is the
alpha channel of the specular map since the does something with it? The
[Engine](Engine "wikilink") page says: *Specular mapping (color and
intensity)*, so maybe the alpha channel is the intensity?

### Physical map

Occlusion seems to not be implemented in engine yet. Roughness and
Metalness is.

## Material manuals

Those material manuals are from other games, though a big part of them
is compatible, they may even be incomplete even for the original game
they were written for.

- [Q3A Shader
  Manual](https://icculus.org/gtkradiant/documentation/Q3AShader_Manual/),
  The must be 100% compatible with it, if it isn't, it's a bug, please
  report!
  The Dæmon engine may provide more efficient ways to do things anyway
  (for example via the use of pre-collapsed stages).
- [XreaL Shader
  Manual](https://tremap.xtr3m.net/__Games/Xreal/Manual_Shader_1/ShaderManual.htm),
  The may not implement everything, or may implement it in another
  way.
  If you need something listed in the XreaL manual but it does not work
  when you try to use it, please report a feature request.

## Material syntax

The material syntax is inherited from Quake 3 and Doom 3, but the also
received fixes for design regressions introduced in Doom 3 (components
like `normalMap` can be staged).

Keywords prefixed with `q3map_` prefixes are map compiler keywords
([Q3map2](Tools_Q3map2 "wikilink")), keywords prefixed with `qer_` are
editor keywords ([NetRadiant](Tools_NetRadiant "wikilink"), its ancestor
was named *QERadiant*, *QE* dates back from *Quake* with *QuakeEd*).

There are other keywords not having prefixes for historical reasons like
`cull`, `nopicmip`, `nonsolid`, `trans`, etc. Some may be compiler
keywords, others may be engine keywords. The `surfaceparm` keyword may
be read and may be used (or not) by both compiler and engine, they may
affect surfaces or content of brushes with faces having this material on
its sides.

Comments are preceded with `//`.

Here is an example of material file defining three materials:

    // this is a material name (to be applied on a surface):
    textures/shared_vega/plasma_whirl
    // this block is a material definition (a single-staged one):
    {
        // those are optional per-material editor, compiler or renderer keywords:
        qer_editorImage textures/shared_vega_src/plasma_whirl_p

        q3map_surfacelight 150
        q3map_lightRGB 0 .95 0
        q3map_globaltexture

        surfaceparm nonsolid
        surfaceparm noimpact
        surfaceparm nomarks

        cull none

        deformVertexes wave 64 sin .25 .25 0 .5

        // this block is a stage definition:
        {
            // this is a texture keyword with a texture path:
            map textures/shared_vega_src/plasma_whirl_b

            // those are optional per-stage renderer keywords:
            tcMod rotate 20
            blend blend
        }
    }

    // this is another material name:
    textures/shared_ex/base1a
    // this block is another material definition (a multitextured one):
    {
        // those is an optional per-material editor keyword:
        qer_editorImage     textures/shared_ex_src/base1a_d

        // this block is a stage definition,
        // it is called a pre-collapsed stage as diffuse, normal
        // and (implicit) lightmap stages are done within a single stage:
        {
            diffuseMap      textures/shared_ex_src/base1a_d
            normalMap       textures/shared_ex_src/base1_n
            heightMap       textures/shared_ex_src/base1_h
            specularMap     textures/shared_ex_src/base1_s
        }
    }


    // this is another material name:
    textures/thunder_custom/ter_rocksand_yz
    // this block is another material definition (a multi-staged one):
    {
        // those are optional per-material editor and compiler keywords:
        qer_editorImage textures/thunder_custom_src/ter_rocksand_p

        q3map_nonplanar
        q3map_shadeAngle 90
        q3map_tcGen ivector ( 0 256 0 ) ( 0 0 256 )
        q3map_alphaMod dotproduct2 ( 0 0 .75 )

        // this block is a pre-collapsed stage definition:
        {
            // those are a texture component keywords with texture paths:
            diffuseMap  textures/shared_pk02_src/rock01_d
            normalMap   textures/shared_pk02_src/rock01_n
            specularMap textures/shared_pk02_src/rock01_s

            // those are optional per-stage renderer keywords:
            rgbGen identity
        }

        // this block is another pre-collapsed stage definition:
        {
            // those are a texture component keywords with texture paths:
            diffuseMap  textures/shared_pk02_src/sand01_d
            normalMap   textures/shared_pk02_src/sand01_n
            specularMap textures/shared_pk02_src/sand01_s

            // those are optional per-stage renderer keywords:
            blendFunc blend
            alphaGen vertex
        }
    }

## Material examples

### Simple materials

This material features a pure white diffuse map and lightmap will not be
baked on it, engine will not draw weapon impacts and other marks.

    textures/vega_custom/white
    {
        qer_editorImage textures/vega_custom_src/white_d

        {
            diffuseMap textures/vega_custom_src/white_d
        }

        surfaceparm nomarks
        surfaceparm nolightmap
    }

This environmental texture features a diffuse map, a normal map, an
height map and a specular map.

    textures/shared_ex/base1a
    {
        qer_editorImage     textures/shared_ex_src/base1a_d

        {
            diffuseMap      textures/shared_ex_src/base1a_d
            normalMap       textures/shared_ex_src/base1_n
            heightMap       textures/shared_ex_src/base1_h
            specularMap     textures/shared_ex_src/base1_s
        }
    }

This player model texture features a diffuse map, a normal map, and a
specular map. The engine will not reduce its resolution to side size
below `256` pixels to keep details readable.

    models/players/level4/level4b
    {
        qer_editorImage models/players/level4/level4b_d
        imageMinDimension 256
        {
            diffuseMap  models/players/level4/level4b_d
            normalMap   models/players/level4/level4b_n
            specularMap models/players/level4/level4b_s
        }
    }

### Graphical effects materials

This buildable material features a diffuse map, a normal map and a
specular map, and two stages for glow maps with custom blending
functions. The top glow map is waving using a sine function, the around
glow map uses a custom per-color-channel blending function.

When the buildable is destroyed, another material is used instead which
only features a diffuse map, a normal map and a specular map.

The engine will not reduce the image to side lower than `128` to keep
details readable.

    models/buildables/drill/drill
    {
        qer_editorImage models/buildables/drill/drill_d
        imageMinDimension 128
        {
            diffuseMap  models/buildables/drill/drill_d
            normalMap   models/buildables/drill/drill_n
            specularMap models/buildables/drill/drill_s
        }
        // white lamp on top
        {
            map models/buildables/drill/drill_top_a
            blendfunc add
            rgbGen    wave sin 1 .85 .5 .08
        }
        // small yellow lamps around
        {
            map models/buildables/drill/drill_around_a
            blendfunc add
            rgb       .85 .85 .85
        }
        when destroyed models/buildables/drill/drill_dead
    }

    models/buildables/drill/drill_dead
    {
        qer_editorImage models/buildables/drill/drill_d
        imageMinDimension 128
        {
            diffuseMap  models/buildables/drill/drill_d
            normalMap   models/buildables/drill/drill_n
            specularMap models/buildables/drill/drill_s
        }
    }

This material is a non-solid double-sided (not culled) translucent
rotating material emitting light, the surface will be deformed like
waves and no impact will be drawn on it.

    textures/shared_vega/plasma_whirl
    {
        qer_editorImage textures/shared_vega_src/plasma_whirl_p

        q3map_surfacelight 150
        // radioactive green #00f200
        q3map_lightRGB 0 .95 0
        q3map_globaltexture

        surfaceparm nonsolid
        surfaceparm noimpact
        surfaceparm nomarks

        cull none

        // deformVertexes wave <div> <func> <base> <amplitude> <phase> <freq>
        deformVertexes wave 64 sin .25 .25 0 .5

        {
            map textures/shared_vega_src/plasma_whirl_b
            tcMod rotate 20
            blend blend
        }
    }

This material is a double-sided, non solid, moving water texture, with a
scaling and scrolling effects applied. Surface is also deformed.

If a player manages to go enter a brush using this material, the player
view will be affected by in-water view effect.

    textures/shared_vega/water
    {
        qer_editorImage textures/shared_vega_src/water_p
        qer_trans .5

        surfaceparm nonsolid
        surfaceparm water
        cull none

        q3map_globaltexture

        deformVertexes wave 64 sin .25 .25 0 .5

        {
            map textures/shared_vega_src/water_b
            blendFunc GL_dst_color GL_one
            rgbGen identity
            tcMod scale .5 .5
            tcMod scroll .01 .01
        }
    }

### Translucent materials

This glass material features a diffuse map and is translucent. The
engine will render things behind this surface.

In [NetRadiant](Tools_NetRadiant "wikilink") editor, the image will be
rendered with a `50%` translucency (`0.50`/1). The editor renderer is
not as advanced as a game engine and does not support blending, that's
why we use simpler tricks like half translucency in editor.

This texture is double-sided (not `cull`ed) and considered as
`trans`lucent by the [Q3map2](Tools_Q3map2 "wikilink") map compiler
(surfaces behind will not be removed from BSP tree so the engine will
render them). When baking lightmaps with
[Q3map2](Tools_Q3map2 "wikilink"), the casted light going through this
texture will be affected by this texture, producing shadows with
darkness relative to the alpha channel of the glass texture.

    textures/shared_trak5/glass
    {
        qer_editorImage     textures/shared_trak5_src/glass_d
        qer_trans           0.50

        cull                none
        surfaceparm         alphashadow
        surfaceparm         trans

        {
            diffuseMap  textures/shared_trak5_src/glass_d
            blend blend
        }
    }

This grate floor material features a diffuse map, a normal map and a
specular map.

The [Q3map2](Tools_Q3map2 "wikilink") map compiler will keep visible the
surfaces behind and when computing lightmaps, it will cast shadows based
on the diffuse map alpha channel.

The engine will not draw weapon impacts and other marks on it. The
engine will not blend the texture, instead, it will consider opaque
everything that is greater or equal (`GE`) to `128` (from `0` to `256`).
Other options are `GT0` (greater than `0`) or `LT128` (less then `128`).

Because of the `nopicmip` keyword, this textures will always be
displayed in full resolution (you may prefer using `imageMinDimension`
keyword instead, to only set a minimum value to not reduce the
resolution below it).

The game will play metal step sounds when a player walks on it.

    textures/perseus_pk02/floor07
    {
        qer_editorImage textures/perseus_pk02_src/floor07_d

        surfaceparm trans
        surfaceparm nomarks
        surfaceparm metalsteps
        surfaceparm alphashadow
        nopicmip

        {
            diffuseMap  textures/perseus_pk02_src/floor07_d
            normalMap   textures/perseus_pk02_src/floor07_n
            specularMap textures/perseus_pk02_src/floor07_s
            alphafunc GE128
        }
    }

### Light-emitting materials

This material for a star chart to be displayed on a wall only features a
diffuse map and emits a light with an intensity of `150` and no lightmap
will be baked on it.

    textures/vega_custom/starchart01
    {
        qer_editorImage textures/vega_custom_src/starchart01_d

        q3map_surfacelight 150

        surfaceparm nolightmap

        {
            map textures/vega_custom_src/starchart01_d
        }
    }

This is a light-emitting material for the surface of a soda vending
machine front. It features a diffuse map, a normal map, an height map
(adding relief to buttons and other things), a specular map, and a glow
map.

The emitted light is an arbitrary RGB color (with floats from `0.0` to
`1.0`)

The emitted light intensity is `150`, a light is emitted every `64`
unit, the backSplash light (a specific light added to lit back the
surface) has an intensity that is `100`% the one of the light and is
positioned at `20` quake units in front of the surface.

    textures/shared_ambient/soda-machines/khalsacola
    {
        qer_editorImage         textures/shared_ambient_src/soda-machines/khalsacola_d

        q3map_lightRGB          .392 .235 .392
        q3map_lightSubdivide    64
        q3map_surfaceLight      150
        q3map_backSplash        100 20

        {
            diffuseMap      textures/shared_ambient_src/soda-machines/khalsacola_d
            heightMap       textures/shared_ambient_src/soda-machines/khalsacola_h
            normalMap       textures/shared_ambient_src/soda-machines/khalsacola_n
            normalFormat    X Y Z
            specularMap     textures/shared_ambient_src/soda-machines/khalsacola_s
            glowMap         textures/shared_ambient_src/soda-machines/khalsacola_a
        }
    }

This is a light-emitting material for a door surface. It feature a
diffuse map, a normal map, and height map, a specular map and a glow
map. The emitted light is averaged from the glow map.

The light intensity is `50`. The backSplash light values are the default
ones (`5`%, `23` qu).

    textures/shared_pk01/door01a_50
    {
        qer_editorImage     textures/shared_pk01_src/door01a_d

        q3map_surfacelight  50
        q3map_lightImage    textures/shared_pk01_src/door01_a

        {
            diffuseMap      textures/shared_pk01_src/door01a_d
            normalMap       textures/shared_pk01_src/door01_n
            heightMap       textures/shared_pk01_src/door01_h
            specularMap     textures/shared_pk01_src/door01_s
            glowMap         textures/shared_pk01_src/door01_a
        }
    }

### Terrain blending materials

This is a material featuring two stages. The first stage featuyes one
rock texture with diffuse, normal and specular maps. The second stage
features one sand texture with diffuse, normal, specular maps. Those two
stages are blended together by the engine according to the alphaGen
vertex value of the surface (computed by the
[Q3map2](Tools_Q3map2 "wikilink") tool) allowing a rocky surface to
smoothly fade to sand surface. This is useful for example blend some
rocks into a sandy floor.

The preview image is custom.

    textures/thunder_custom/ter_rocksand_yz
    {
        qer_editorImage textures/thunder_custom_src/ter_rocksand_p

        q3map_nonplanar
        q3map_shadeAngle 90
        q3map_tcGen ivector ( 0 256 0 ) ( 0 0 256 )
        q3map_alphaMod dotproduct2 ( 0 0 .75 )

        {
            diffuseMap  textures/shared_pk02_src/rock01_d
            normalMap   textures/shared_pk02_src/rock01_n
            specularMap textures/shared_pk02_src/rock01_s
            rgbGen identity
        }
        {
            diffuseMap  textures/shared_pk02_src/sand01_d
            normalMap   textures/shared_pk02_src/sand01_n
            specularMap textures/shared_pk02_src/sand01_s
            blendFunc blend
            alphaGen vertex
        }
    }

### Materials reusing textures

Those two ceiling material variants have specific diffuse and specular
maps but reuse the same normal map.

    textures/shared_ej01-clean/ceiling01
    {
        qer_editorImage textures/shared_ej01-clean_src/ceiling01_d

        {
            diffuseMap  textures/shared_ej01-clean_src/ceiling01_d
            normalMap   textures/shared_ej01-common_src/ceiling01_n
            specularMap textures/shared_ej01-clean_src/ceiling01_s
        }
    }

    textures/shared_ej01-ice/ceiling01
    {
        qer_editorImage textures/shared_ej01-ice_src/ceiling01_d

        {
            diffuseMap  textures/shared_ej01-ice_src/ceiling01_d
            normalMap   textures/shared_ej01-common_src/ceiling01_n
            specularMap textures/shared_ej01-ice_src/ceiling01_s
        }
    }

This material is a light-emitting one with diffuse, normal, specular and
glow maps. The normal map uses a custom `-X -Y Z` normal map format.

The glow map uses a dedicated stage using a blending function to only
make the red channel glowing. This means another material can reuse the
exact same image but glow in green or blue or yellow by using other RGB
blending values.

One can do another material reusing the exact same textures with another
intensity and/or another color by modifying `q3map_surfacelight` and
`q3map_lightRGB` and modifying material name to reflect the changes.

    textures/vega_custom/squarelight01_red_150
    {
        qer_editorImage textures/shared_vega_src/squarelight01_red_p

        // red
        q3map_lightRGB 1 0 0
        q3map_surfacelight 150

        {
            diffuseMap  textures/shared_vega_src/squarelight01_d
            normalMap   textures/shared_vega_src/squarelight01_n
            normalFormat -X -Y Z
            specularMap textures/shared_vega_src/squarelight01_s
        }
        {
            map         textures/shared_vega_src/squarelight01_a
            blendFunc add
            red   1
            green 0
            blue  0
        }
    }

[Category:Formats](Category:Formats "wikilink")
[Category:Texturing](Category:Texturing "wikilink")
[Category:Mapping](Category:Mapping "wikilink")
[Category:Modeling](Category:Modeling "wikilink")