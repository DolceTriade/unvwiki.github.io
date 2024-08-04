---
title: Formats Model
permalink: /Formats/Model/
---

## Tutorials

See [Tutorials#Modeling](Tutorials#Modeling "wikilink").

## Tools

See [Tools/Modeling](Tools_Modeling "wikilink") and
[Tools/IQM](Tools_IQM "wikilink").

While members of the team may have used Zbrush, 3ds Max, Maya, and other
software, [Blender](Tools_Blender "wikilink") is preferred as it is used
by most of the team and is freely available, making it accessible to
anyone.

Using software other than Blender can create problems in collaborating
on work. Please be aware that in transferring data between software some
information may be lost, such as animation data. At a minimum,
transferring model and UV (unwrap) data is almost guaranteed with the
Wavefront `.obj` format.

When doing props for maps, some people may prefer doing them in
[NetRadiant](Tools_NetRadiant "wikilink") the same way they do their
maps, see [Mapping](Mapping "wikilink").

## Licensing

The following licenses are suitable for models:

## Supported formats

When you produce a model with an editor like
[Blender](Tools_Blender "wikilink"), you'll better convert it to IQM,
see [IQM#Tools](IQM#Tools "wikilink") for Blender importer and exporter.
You can them convert the IQM file to IQE, see `iqm_to_iqe.py` from
[asstools](IQM#asstools "wikilink").

When you produce a model with an editor like
[NetRadiant](Tools_NetRadiant "wikilink"), you usually compile the
`.map` file to BSP with [Q3map2](Tools_Q3map2 "wikilink") then convert
the BSP to ASE or OBJ using Q3map2. It's possible to convert directly
from `.map` to ASE or to OBJ but the model will not be optimized when
doing so.

See also [Exporting models](Exporting_models "wikilink").

### Supported formats for rendering in engine

- [IQM](IQM "wikilink"), a model format with skeletal animation, can
  embed multiple meshes and animations in one file, ;
- [MD5](Formats_MD5 "wikilink") (MD5Mesh, MD5Anim), a model format with
  skeletal animation, every mesh and animation are stored is separate
  files;
- [MD3](Formats_MD3 "wikilink"), a model format with vertex animation, .

### Supported formats for baking in maps

- [IQM](IQM "wikilink");
- [MD3](Formats_MD3 "wikilink");
- OBJ;
- ASE.

## Recommended formats

### In repositories

It's recommended to store model sources as compress `.blend` files.
Either you tick the compression option in Blender when saving, either
you recompress them with `gzip` tool and rename the `.blend.gz` to
`.blend` (that's basically what Blender does when you enable
compression).

It's required to also store the model in an non-modeler-specific format
in repository.

Models to be baked in maps must be stored in a format like IQE so the
[Urcheon](Tools_Urcheon "wikilink") tool can convert them to IQM
supported by the [NetRadiant](Tools_NetRadiant "wikilink") editor and
the [Q3map2](Tools_Q3map2 "wikilink") map compiler, or in a format like
MD3, OBJ or ASE.

Models to be loaded by the engine in maps must be stored in a format
like IQE so the [Urcheon](Tools_Urcheon "wikilink") tool can convert
them to IQM supported by the [Dæmon engine](Engine "wikilink"), or in a
format like MD5, or MD3.

When storing models in repositories prefer text formats like IQE, MD5,
ASE or OBJ over binary formats like MD3.

When possible, prefer IQE.

## Software-specific help

- [Blender](Tools_Blender "wikilink");
- [NetRadiant](Tools_NetRadiant "wikilink").

## Workflow overview

The process from start to finish typically goes like this:

1.  **Modeling** — A 3D model is created in any of a number of
    applications; you do not need to worry about what software you use
    for this stage as long as it can export in a format such as
    Wavefront .obj. At this stage, it may be either high or low-poly.
2.  **Texturing** — The model is unwrapped and textured. If a high-poly
    model is available, its normals are baked onto the low-poly model.
3.  **Rigging** — The model is rigged. From this point forward, if the
    unwrap (and texture) is to be changed, this must be done in the same
    program that animation is being done in.
4.  **Animation** — The model is animated. If you are using Blender,
    simply animate the model with its different animations in different
    keyframe ranges. The order is unimportant. For example, the death
    animation might occupy frames 0-60 and the pain animation occupy
    frames 61-120. See [the list of animation
    names](Exporting_Models#Animation_names "wikilink") for more
    information as to what animations must be made for each model. Also,
    when using Blender, have the model face in the +Y direction. The
    newer MD5 exporter has an option to reorient the model to face in
    the +X direction.
5.  **Exporting** — The engine obviously cannot read .blend files, so
    the model must be exported to another format that it understands.
    IQM is currently the preferred format. The process for doing this is
    described in detail on the [Exporting
    Models](Exporting_Models "wikilink") page. This is a multi-step
    process involving configuration editing and
    [packaging](Packaging_game_data "wikilink").

[Category:Formats](Category:Formats "wikilink")
[Category:Modeling](Category:Modeling "wikilink")