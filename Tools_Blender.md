---
title: Tools Blender
permalink: /Tools/Blender/
---

Blender is a cross-platform 3D modeler and animator (and much more)
available for GNU/Linux, macOS, Windows and more operating systems.

Blender is free software and is the recommended way to edit and animate
models for Unvanquished.

## Website

The Blender website is [blender.org](https://www.blender.org).

The Blender documentation can be found on
[docs.blender.org/manual](https://docs.blender.org/manual/en/latest/).

The Blender source repository is
[github.com/blender/blender](https://github.com/blender/blender).

## Features

Blender is a very large and complex piece of software. For working on
Unvanquished, we suggest using the latest version.

If you are still using 2.4 because you are comfortable with its GUI,
make the switch! There are too many new features to take advantage of
not to, and it will be easier to work with other artists on the team if
you do.

## Organizing Large Files

### Vertex Groups

- Keep your vertex groups organized by name. If there are too many
  vertex groups to do this by hand, open a python console and use the
  following command at the prompt after selecting the object whose
  vertex group names are to be sorted:
       >>> bpy.ops.object.vertex_group_sort()
- Do not create vertex groups for bones that are not intended to deform
  the mesh.
- When parenting an armature to a mesh, **do not** select "With
  Automatic Weights". This may save you the time of creating vertex
  groups, but you will likely have groups that you do not want, such as
  for pose bones (i.e., those that manipulate other bones indirectly
  with constraints but are not intended to deform the mesh), or will
  assign too many vertex weights to vertices. (The daemon engine, for
  performance reasons, only supports four weights per vertex.)

### Naming Conventions for Objects

Name objects using a period-delimited (`.`) hierarchy. Generally
speaking, name datablocks with the same name as the object but with a
`.d` suffix to distinguish them from objects.

For example:

- Leg.Upper.Left
- Leg.Upper.Right
- Leg.Lower.Left
- Leg.Lower.Right

You are free to organize this hierarchy however you see fit, but please
be consistent.

In some instances, using the suffixes `_L` and `_R` instead of `.Left`
and `.Right` may be necessary for certain features to work. This is also
acceptable.

### Managing Textures

Place all textures in a subdirectory named "Textures". Ensure that your
file paths in Blender use the matching case so that users on
case-sensitive filesystems will not have problems.

Use [relative file paths](#relative "wikilink") for textures, and the
following naming convention:

<span style="color:#74B6C7;">`Name`</span>`_`<span style="color:#CAB527;">`TextureType`</span>`[_`<span style="color:#CA274D;">`AlternateResolution`</span>`].`<span style="color:#79D263">`format`</span>

- **Name** — (Required) The name of the model. If the model is a
  character class or weapon, use that name.
- **TextureType** — (Required) A name indicating the type of information
  the texture contains. Please use one of the following:
  | <var>TextureType</var> | Description                          |
  |------------------------|--------------------------------------|
  | `Alpha`                | An alpha map.                        |
  | `Diffuse`              | The diffuse (albedo) color.          |
  | `DiffuseAlpha`         | A diffuse map with an alpha channel. |
  | `Glow`                 | A glow map.                          |
  | `Normal`               | A normal map.                        |
  | `SpecValue`            | A specular color map.                |
  | `SpecHilight`          | A specular hilight map.              |
  |                        |                                      |
- **AlternateResolution** — (Optional) The resolution of the texture in
  the form
  <span style="color:#74B6C7;">Width</span>x<span style="color:#CAB527;">Height</span>.
  Only include the resolution of the texture in the name if there are
  multiple resolutions to choose from.
- **format** — (Required) The format of the image. For JPEG images, the
  `jpg` extension is preferred over `jpeg` for consistency.

#### Do's and Don'ts

- **Don't** create a diffuse texture without appending `_Diffuse` to the
  name.
- **Don't** create a stand-alone alpha map that is not in greyscale; if
  you create a stand-alone alpha map with an alpha channel containing
  alpha, the filesize will only be larger (if only slightly).

## Tips and Tricks

- The desired playback framerate can be set under Properties → Render →
  Dimensions → Frame Rate.

- When sharing work between computers, use relative filepaths. Start a
  pathname with "//" and Blender looks starting relative to the folder
  that the .blend file is in.

## Troubleshooting

### White marks are visible around the edges of alpha-mapped textures

Enable "Premultiply Alpha".

## Python Scripting

Please see the [full article](Blender_Python_Scripting "wikilink").

## Extensions

### Blender 2.4

- [A collection of Blender 2.4
  extensions](http://wiki.blender.org/index.php/Extensions:2.4/Py/Scripts/249_Extensions)

### Blender 2.5/2.6

- [2.6 scripts
  catalog](http://wiki.blender.org/index.php/Extensions:2.6/Py/Scripts)

Note that the Blender Python API is constantly in flux, so these may or
may not work with newer versions of Blender than they were written for.

#### Import/Export

| Purpose | Format | Last updated | Known to work with | Link                                                                  | Notes                                                                                                                                                                                                                                                                                                                            |
|---------|--------|--------------|--------------------|-----------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Export  | MD5    | Unknown      | 2.59 (partially)   | [katsbits.com](http://www.katsbits.com/smforum/index.php?topic=178.0) | <span style="color:#f00;">Warning: this exporter does not work with newer versions of Blender, and never worked very well to begin with!</span> There is a newer exporter that you should use instead. Please see the [exporting guide](Exporting_Models#Acquiring_and_installing_the_exporter "wikilink") for more information. |
| Import  | MD5    | Unknown      | Unknown            | [katsbits.com](http://www.katsbits.com/smforum/index.php?topic=358.0) | None.                                                                                                                                                                                                                                                                                                                            |
| Export  | MD3    | Unknown      | Unknown            | [xembie.com](http://sourceforge.net/projects/md3exporter/)            | None.                                                                                                                                                                                                                                                                                                                            |
|         |        |              |                    |                                                                       |                                                                                                                                                                                                                                                                                                                                  |

## Resources

- Modeling
- Rigging
- Unwrapping/Texturing
  - [Baking normal
    maps](http://www.katsbits.com/tutorials/blender/baking-normal-maps-from-models.php)
- Blender Python API Docs
  - Release Notes
    - [Blender 2.62 Python Release
      Notes](http://wiki.blender.org/index.php/Dev:Ref/Release_Notes/2.62/Python)
    - [Blender 2.61 Python Release
      Notes](http://wiki.blender.org/index.php/Dev:Ref/Release_Notes/2.61/Python)
    - [Blender 2.60 Python Release
      Notes](http://wiki.blender.org/index.php/Dev:Ref/Release_Notes/2.60/Python)
  - API reference
    - [API reference for Blender
      2.66.0](http://www.blender.org/documentation/blender_python_api_2_66_release/)
      (nothing changed in this release)
    - [API reference for Blender
      2.65.3](http://www.blender.org/documentation/blender_python_api_2_65_3/)
      ([changelog](http://www.blender.org/documentation/blender_python_api_2_65_3/change_log.html#to-2-65))
    - [API reference for Blender
      2.64.5](http://www.blender.org/documentation/blender_python_api_2_64_5/)
      ([changelog](http://www.blender.org/documentation/blender_python_api_2_64_5/change_log.html#to-2-64))
    - [API reference for Blender
      2.63.7](http://www.blender.org/documentation/blender_python_api_2_63_7/)
      ([changelog](http://www.blender.org/documentation/blender_python_api_2_63_7/change_log.html#to-2-63))
    - [API reference for Blender
      2.62.1](http://www.blender.org/documentation/blender_python_api_2_62_1/)
      ([changelog](http://www.blender.org/documentation/blender_python_api_2_62_1/change_log.html#to-2-62))
    - [API reference for Blender
      2.61.0](http://www.blender.org/documentation/blender_python_api_2_61_0/)
      ([changelog](http://www.blender.org/documentation/blender_python_api_2_61_0/change_log.html#to-2-61))
    - [API reference for Blender
      2.59.0](http://www.blender.org/documentation/blender_python_api_2_59_0/)
      ([changelog](http://www.blender.org/documentation/blender_python_api_2_59_0/change_log.html#to-2-59))
  - [Code
    snippets](http://wiki.blender.org/index.php/Dev:2.5/Py/Scripts/Cookbook/Code_snippets)
  - [A user's collection of code
    snippets](http://wiki.blender.org/index.php/User:Kilon/Python_book_of_magic)

[Category:Tools](Category:Tools "wikilink")
[Category:Modeling](Category:Modeling "wikilink")