---
title: Tutorials Exporting models
permalink: /Tutorials/Exporting_models/
---

## Overview

Getting a finished model out of Blender and into the game is a
relatively involved process with a number of possible pitfalls. This
guide aims to describe the process in as much detail as possible to
assist users who have not done it before, or those who have exported
models for other games and would like to know what (if anything) is
different.

If you would like to export from Maya, you may find the official [id
Software documentation](http://www.iddevnet.com/quake4/Animations)
useful.

At present, this guide primarily describes the process for exporting
models to the MD5 format. While the engine supports both MD3 and MD5,
the latter is preferred. The reasons for this are discussed
[below](#What_is_MD5? "wikilink").

Before a model may be exported and used in-game, it must be adequately
prepared:

- [Engine limitations](#Limitations_of_the_engine "wikilink") must be
  adhered to.
- The model must have a texture applied to it. This texture is not
  automagically applied to the model after it is exported and loaded
  in-game, this is only necessary to satisfy the MD5 exporter; that is,
  the game cannot read from the exported model the filename of the
  texture to use.
- The model must be a mesh and must have an armature modifier applied to
  it.
- The armature's bones all must have at least one keyframe.

The actual process of exporting a model is straightforward:

1.  After ensuring that the above requirements are met, the mesh itself
    is exported.
2.  If using the old exporter, each animation is exported separately.
    The new exporter adds support for [batch
    export](#Batch_export_with_the_new_exporter "wikilink") of
    animations.
3.  A [configuration file](#Configuring_the_model "wikilink") specifying
    data such as the bounding box size and vertical offset is written.
    This may include information that is specific to the particular type
    of model (i.e., buildable or player model).
4.  A [shader](#Writing_shaders "wikilink") is written that determines
    how the model is textured in-game.
5.  Finally, after everything is properly named and configured, the
    files are [packaged](Packaging_game_data "wikilink") and placed in
    the correct game data folder to allow it to be loaded in-game.

## What is MD5?

MD5 is the model format created by id Software for Doom 3 which is also
used by Unvanquished. It is an improvement over its predecessor, MD3, in
that it uses bones to pose the model.

### Advantages over MD3

- Unlike MD3, MD5 is bone-based, meaning that instead of storing an
  entire mesh for each frame of animation, there is only one mesh file.
  This single mesh file is deformed using a vertex shader.
- Because there is only one mesh, only one VBO (vertex buffer object)
  needs to be created for each MD5 model. The deformation is performed
  entirely on the GPU, so it is (theoretically) faster than MD3, and
  uses less memory.
- Because the format is in plain-text, it can be easily verified for
  sanity (i.e., to ensure that it was exported correctly and not
  corrupted in some way).

### Disadvantages over MD3

- Some forms of motion are more difficult to achieve; certain animation
  techniques (such as lattices) are not usable.
- Because the format is in plain-text, it takes up more space than it
  needs to, though this is negligible and a MD5 model will typically be
  smaller than the same model in MD3 format as less data is used per
  each frame of animation with MD5 as compared to MD3.

### Limitations of the engine

The engine places certain limitations on the fidelity of your models
when using the MD5 format. These are:

- There may not be more than 128 bones. (Note: this was increased from
  64.)
- There may not be more than 100,000 vertices.
- There may not be more than 10,000 triangles.
- No vertex may belong to more than four vertex groups (i.e., one vertex
  may not be controlled by more than four bones). An error message will
  be displayed in-game if this requirement is not met. A
  [script](#.22R_LoadMD5:_vertex_.25i_requires_more_than_.25i_weights_on_surface_.28.25i.29_in_model_.27.25s.27.22 "wikilink")
  may be used before exporting to check that this limitation is not
  exceeded.

### Limitations of the format

The MD5 format only supports bones. You may not

- Use lattices or any other means of deformation.
- Scale bones.
- Use keyframes on anything other than bone poses. You may, however, set
  keyframes on bone constraint influences or anything else that would
  affect a bone's position or rotation.

Note that you do not have to have a parent/child relationship between
bones. In fact, in some instances, avoiding a parent/child relationship
is necessary to achieve certain effects, such as moving bones around.

## Acquiring and installing the exporter

### MD3

If for some reason you are interested in the MD3 exporter, it is
available from
[SourceForge](http://sourceforge.net/projects/md3exporter/).

### MD5

#### Old exporter

*Please be aware that there are numerous issues with the old exporter
and the newer versions of Blender. See [the troubleshooting
section](#All_or_part_of_the_mesh_appears_to_be_sucked_to_the_center "wikilink")
below for more information. It is strongly recommended that you use the
[new exporter](#New_exporter "wikilink") instead.*

You can download the exporter from [this thread on
katsbits.com](http://www.katsbits.com/smforum/index.php?topic=178.0).
Installation instructions are in the thread.

#### New exporter

As of 15 May 2012, there is another [MD5 exporter available for Blender
2.63+](http://sourceforge.net/projects/blenderbitsbobs/) ([discussion on
katsbits](http://www.katsbits.com/smforum/index.php?topic=404.0)). This
has been found to be superior to the old exporter. Note that portions of
this guide have not yet been updated to reflect the differences in the
new exporter.

dsalt had patched it (see
[repository](http://sourceforge.net/u/dsalt/blenderbitsbobs/)) to allow
each mesh objects to have a custom `q3tex` property to store the shader
name. In the `.md5mesh` file, this will fill the `shader` for the
corresponding mesh.

## Exporting the mesh

### MD5

Note that for buildables and weapons, the filename of the exported mesh
is dictated by the corresponding [configuration
file](#Configuring_the_model "wikilink"). All player models, however,
are hardcoded to look for `body.md5mesh`.

#### Old exporter

*Please be aware that there are numerous issues with the old exporter
and the newer versions of Blender. See [the troubleshooting
section](#All_or_part_of_the_mesh_appears_to_be_sucked_to_the_center "wikilink")
below for more information. It is strongly recommended that you use the
[new exporter](#New_exporter "wikilink") instead.*

1.  Select the armature and the mesh. The order in which you select the
    two does not matter.
2.  Click File → Export → Quake Model 5 (.md5)
3.  On the left shelf that appears in the file prompt, change the
    Exports combo box to "Mesh only." Don't worry about the scale or
    name fields.
4.  Click "Export MD5".

Once this has been completed, you must manually edit the mesh file (the
one with a `.md5mesh` extension) to specify the correct shader to use.

    --- snip ---
    mesh {
        shader "models/buildables/medistat"

        numverts 4
        vert 0 ( 1.000000 0.000000 ) 0 1
        vert 1 ( 0.000000 0.000000 ) 1 1
    --- snip ---

Note that `models/buildables/medistat` is **not** a file path to a
shader; it is the name (again, not filename) of the shader to use. That
is, a shader with the matching name will be used for this model.

To avoid having to do this every time you export the mesh, set the name
of the material applied to the object in Blender to the same as you
edited the md5mesh.

#### New exporter

- Select the mesh to export.
- Click File → Export → MD5 Mesh (.md5mesh).
- Specify the output filename in the dialog, and click "Export MD5MESH".

The exported model is not ready to be used in-game just yet; it must be
manually edited. Open the exported `.md5mesh` file in a text editor, and
manually delete the top three lines of the file (highlighted in red
below):

<span style="color:#f00;">`// Parameters used during export:`
`//   Reorient: True`
`//   Scale: 1.0`</span>
`MD5Version 10`
`commandline ""`

`numJoints 4`
`numMeshes 1`

`joints {`

`...`

<i>`remainder of file omitted for brevity`</i>

Be sure to save the file when you are done. You will also have to do
this for each animation file that you export.

If you do not want to have to do this each time, you can edit the
exporter script. Open the `export_md5.py` script in the `io_scene_md5`
folder where you installed the script, at around line 30, edit this
code:

`def record_parameters(correctionMatrix):`
`    return [`
`    "// Parameters used during export:\n",`
`    "//   Reorient: {}\n".format(bool(correctionMatrix.to_euler()[2])),`
`    "//   Scale: {}\n".format(correctionMatrix.decompose()[2][0])]`

to look like this:

`def record_parameters(correctionMatrix):`
`    return []`

If you are comfortable with applying patches, you may use this:

    @@ -27,10 +27,7 @@
         return pairs

     def record_parameters(correctionMatrix):
    -    return [
    -    "// Parameters used during export:\n",
    -    "//   Reorient: {}\n".format(bool(correctionMatrix.to_euler()[2])),
    -    "//   Scale: {}\n".format(correctionMatrix.decompose()[2][0])]
    +    return []

     def define_components(obj, bm, bones, correctionMatrix):
         scaleFactor = correctionMatrix.to_scale()[0]

Note that you will also have to manually set the shader as with the [old
exporter](#Old_exporter_2 "wikilink").

## Exporting the animations

### MD3

Exported MD3 animations require a configuration file that specifies
which frames of the animation correspond to which actions the game will
display.

This varies slightly by the type (i.e., weapon or buildable) of model.

### MD5

#### Old exporter

*Please be aware that there are numerous issues with the old exporter
and the newer versions of Blender. See [the troubleshooting
section](#All_or_part_of_the_mesh_appears_to_be_sucked_to_the_center "wikilink")
below for more information. It is strongly recommended that you use the
[new exporter](#New_exporter "wikilink") instead.*

The procedure for exporting animations is the same as for exporting the
mesh with regard to selecting the mesh and the armature. Before using
the exporter, however, you must be certain to set the start and end
frames to encompass only the particular animation that you wish to
export; each animation must be exported separately, unless the [new
exporter](#New_exporter "wikilink") is used, which adds a [batch
export](#Batch_export_with_the_new_exporter "wikilink") feature.

<figure>
<img src="Md5_export_timeline.png" title="Md5_export_timeline.png" />
<figcaption>Md5_export_timeline.png</figcaption>
</figure>

At the export file prompt, choose "Anim only." from the "Exports" combo
box. Enter as the filename the name of the particular animation that you
are exporting; the correct names to use are given below.

#### Batch export with the new exporter

The [new exporter](Exporting_Models#Batch_export "wikilink") now
supports batch export of models.

To make use of this feature, you must set [frame
markers](http://wiki.blender.org/index.php/Doc:2.6/Manual/Animation/Markers)
denoting the start and end of each animation. The name of frame markers
denoting the start of an animation must end in "_start" and markers
denoting the end of an animation must end in "_end"; for example, frame
markers denoting the start and end of a buildable's construct animation
would be "construct_start" and "construct_end". Avoid using frame
markers with duplicate names, as which one will be used by the exporter
is not predictable. Note that frame markers may overlap however you
please; this is useful when two animations share a frame or you would
like to automate the process of exporting the same few frames of
animation as several different animation files (e.g., for testing
purposes).

All operations in modifying frame markers are performed in the
[timeline](http://wiki.blender.org/index.php/Doc:2.6/Manual/Animation/Timeline):

- To create a frame marker, move the timeline to the desired frame and
  press <span class="hotkey">M</span>.
- To select a frame marker, click with the right mouse button.
- To move a frame marker, select it and press
  <span class="hotkey">G</span>.
- To delete a frame marker, select it and press
  <span class="hotkey">X</span>.
- To rename a frame marker, select it and press
  <span class="hotkey">Ctrl</span><span class="hotkey">M</span>.

The actual exportation process becomes much simpler:

1.  Click File → Export → MD5 (batch export).
2.  Specify the filename of the `.md5mesh` to export.

## Animation names

The filenames for each exported animation must be what the engine
expects for it to be able to load them, and vary depending on the format
(MD3 or MD5) and type (e.g., buildable, weapon, or player) of model
being exported.

### Weapons

Note that for both MD3 and MD5 models, there may be separate models for
first- and third-person views. Please see "[Configuring the
model](#Weapons "wikilink")" for more information regarding how to
specify separate models.

#### MD3

MD3 does not use separate files for separate animations. Instead, a
configuration file specifies what frames of a single MD3 animation are
used for each in-game animation.

In addition to the base weapon mesh, there may be as many as three
additional MD3 meshes:

| Search string   | Tag          | Description                                                                     |
|-----------------|--------------|---------------------------------------------------------------------------------|
| `%s_flash.md3`  | `tag_flash`  | The weapon's muzzle flash.                                                      |
| `%s_barrel.md3` | `tag_barrel` | The weapon's barrel.                                                            |
| `%s_hand.md3`   | N/A          | Hands holding the weapon model. Note: this is not used for third person models. |

For non-programmers, the `%s` string is replaced by the parameter given
to the `weaponModel` or `weaponModel3rdPerson` keyword.

The tag `tag_weapon` is used on the main weapon model to align the third
person weapon model to the third person player model.

#### MD5

Note that each animation filename must have the `.md5anim` extension.

| Animation name   | Engine constant | Description                                                                                                                                              |
|------------------|-----------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| `%s_view_idle`   | `WANIM_IDLE`    | Animation played when a weapon is not being fired                                                                                                        |
| `%s_view_lower`  | `WANIM_DROP`    | Animation played when a weapon is being put away                                                                                                         |
| `%s_view_reload` | `WANIM_RELOAD`  | Weapon reload animation                                                                                                                                  |
| `%s_view_raise`  | `WANIM_RAISE`   | Animation played when a weapon is switched to                                                                                                            |
| `%s_view_fire`   | `WANIM_ATTACK1` | Default attack animation                                                                                                                                 |
|                  | `WANIM_ATTACK2` | Usage of these is highly dependent on the player class. The marauder, for example, may randomly use one of these instead of `WANIM_ATTACK1`.<sup>1</sup> |
|                  | `WANIM_ATTACK3` |                                                                                                                                                          |
|                  | `WANIM_ATTACK4` |                                                                                                                                                          |
|                  | `WANIM_ATTACK5` |                                                                                                                                                          |
|                  | `WANIM_ATTACK6` |                                                                                                                                                          |
|                  | `WANIM_ATTACK7` |                                                                                                                                                          |
|                  | `WANIM_ATTACK8` |                                                                                                                                                          |
|                  |                 |                                                                                                                                                          |

1.  See `PM_Weapon()`.

### Buildables

#### MD3

As always, MD3 buildable models require a separate configuration file
that specifies which frames of the animation correspond to actions
displayed by the game.

Each line in the configuration file corresponds to a single animation.
Those animations are in the same order as in the table for MD5 animation
names below.

The order that animations appear in the configuration file must match
this order exactly. Animations may not be omitted.

The syntax is as follows:

<var>`firstFrame`</var>` `<var>`numFrames`</var>` [`<var>`loopFrames`</var>` [`<var>`fps`</var>`]]`

- <var>firstFrame</var> — Specifies the initial frame of the animation.
- <var>numFrames</var> — Specifies the number of frames following the
  initial frame that comprise that animation.
- <var>loopFrames</var> — (*Optional*)
- <var>fps</var> — (*Optional, may only be used if loopFrames is
  specified*) Specifies the framerate of the animation. If not
  specified, defaults to 1.

C and C++ style comments (i.e., `//` and `/* */`) are permitted past the
last argument.

#### MD5

As with weapon animations, each animation filename must have the
`.md5anim` extension.

| Animation name      | Engine constant           | Used by                                     | Description                                                                                                                                                                                           |
|---------------------|---------------------------|---------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `idle`              | `BANIM_IDLE1`             | All                                         | Idle animation, shown when the buildable is not doing anything (or unpowered in case of human buildables). They are used in place of other animations when they are missing (unless otherwise noted). |
| `idle2`             | `BANIM_IDLE2`             | Medistation, telenode, barricade, egg       | ‘Active’ idle state, e.g. while the medistation is currently healing (but not when transitionning from or to healing state).                                                                          |
| `powerdown`         | `BANIM_POWERDOWN`         | Human buildables, (barricade)               | Animation played at the moment a buildable loses power.                                                                                                                                               |
| `idle_unpowered`    | `BANIM_IDLE_UNPOWERED`    | Human buildables, (barricade)               | Idle animation played when a buildable is unpowered. *(Formerly `idle3`.)*                                                                                                                            |
| `construct`         | `BANIM_CONSTRUCT1`        | All                                         | Construction animation, shown when the buildable is being built.                                                                                                                                      |
| `construct2`        | `BANIM_CONSTRUCT2`        | Medistation, (telenode), (egg)              | Animation played when returning to the primary idle state, for example after a medistation has healed.                                                                                                |
| `attack`            | `BANIM_ATTACK1`           | All (except tesla)                          | Animation played when a buidlable is attacking or transitioning to its ‘active’ idle state. For the barricade, the animation when it is shrinking.                                                    |
| `attack2`           | `BANIM_ATTACK2`           | (Medistation), (telenode), barricade, (egg) | Unshrink animation for the barricade, it falls back on `BANIM_ATTACK1`.                                                                                                                               |
| `spawn`             | `BANIM_SPAWN1`            | Telenode, Egg                               | Animation for when when a player spawns from a spawn buildable like an egg or a telenode.                                                                                                             |
| `spawn2`            | `BANIM_SPAWN2`            | Currently unused.                           |                                                                                                                                                                                                       |
| `pain`              | `BANIM_PAIN1`             | All                                         | Default pain animation, used when a buildable is damaged.                                                                                                                                             |
| `pain2`             | `BANIM_PAIN2`             | (Medistation), barricade, (egg)             | Pain animation used for the barricade when it is damaged and shrunk. It falls back on `BANIM_PAIN1`.                                                                                                  |
| `destroy`           | `BANIM_DESTROY1`          | All                                         | Played when a buildable is killed or destroyed.                                                                                                                                                       |
| `destroy_unpowered` | `BANIM_DESTROY_UNPOWERED` | All which can be unpowered                  | Played when an unpowered buildable is killed or destroyed. It falls back on `BANIM_DESTROY1`.                                                                                                         |
| `destroyed`         | `BANIM_DESTROYED`         | All                                         | The animation played between the buildable's destroy animation and the blow up. At this point the is in a dead state. The barricade reuses the shrunk state animation.                                |
|                     |                           |                                             |                                                                                                                                                                                                       |

*Note: buildables whose names are in (parentheses) may not actually use
the animation but the animations are loaded. Maybe one day it is
possible those animations well be used.*

### Player models

#### MD5

As with weapon animations, each animation filename must have the
`.md5anim` extension.

Items in italics need to be double-checked.

Note that at present, some of these strings do not match the constants.

| Animation name    |                  |                  | Engine constant |                 |
|-------------------|------------------|------------------|-----------------|-----------------|
| Assumed Correct   | Actual (Humans)  | Actual (Aliens)  | Humans          | Aliens          |
| `attack`          | `attack`         | `attack`         | `TORSO_ATTACK`  | `NSPA_ATTACK1`  |
| `attack2`         | `idle`           | `attack2`        | `TORSO_ATTACK2` | `NSPA_ATTACK2`  |
| `attack3`         | `attack3`        | `attack3`        | N/A             | `NSPA_ATTACK3`  |
| `charge`          | N/A              | `charge`         | N/A             | `NSPA_CHARGE`   |
| `crouch`          | `crouch`         | N/A              | `LEGS_IDLECR`   | N/A             |
| `crouch_backward` | `crouch_forward` | N/A              | `LEGS_BACKCR`   | N/A             |
| `crouch_forward`  | `crouch_forward` | N/A              | `LEGS_WALKCR`   | N/A             |
| `die`             | `die`            | `die`            | `BOTH_DEATH1`   | `NSPA_DEATH1`   |
| `gesture`         | `gesture`        | `gesture`        | `TORSO_GESTURE` | `NSPA_GESTURE`  |
| `idle`            | `idle`           | N/A              | `LEGS_IDLE`     | N/A             |
| `jump`            | `jump`           | `jump`           | `LEGS_JUMP`     | `NSPA_JUMP`     |
| `jump_back`       | `jump`           | `jump_back`      | `LEGS_JUMPB`    | `NSPA_JUMPBACK` |
| `land`            | `land`           | `land`           | `LEGS_LAND`     | `NSPA_LAND`     |
| `land_back`       | `land`           | `land_back`      | `LEGS_LANDB`    | `NSPA_LANDBACK` |
| `pain1`           | N/A              | `pain1`          | N/A             | `NSPA_PAIN1`    |
| `pain2`           | N/A              | `pain2`          | N/A             | `NSPA_PAIN2`    |
| `run`             | `run`            | `run`            | `LEGS_RUN`      | `NSPA_RUN`      |
| `run_backwards`   | `run` (?)        | `run_backwards`  | `LEGS_BACK`     | `NSPA_RUNBACK`  |
| `run_left`        | N/A              | `run_left`       | N/A             | `NSPA_RUNLEFT`  |
| `run_right`       | N/A              | `run_right`      | N/A             | `NSPA_RUNLEFT`  |
| `stand`           | `?`              | `stand`          |                 | `NSPA_STAND`    |
| `stand2`          | `idle`           |                  | `TORSO_STAND2`  |                 |
| `step`            | `step`           |                  | `LEGS_TURN`?    |                 |
| `swim`            | `swim`           | `swim`           | `LEGS_SWIM`     | `NSPA_SWIM`     |
| `turn`            | `step`           |                  | `LEGS_TURN`     |                 |
| `walk`            | `walk`           | `walk`           | `LEGS_WALK`     | `NSPA_WALK`     |
| `walk_backwards`  | `walk`           | `walk_backwards` | `LEGS_BACKWALK` | `NSPA_WALKBACK` |
| `walk_left`       | N/A              | `walk_left`      | N/A             | `NSPA_WALKLEFT` |
| `walk_right`      | N/A              | `walk_right`     | N/A             | `NSPA_WALKLEFT` |
|                   |                  |                  |                 |                 |

## Writing shaders

{{Note\|See the [Formats/Material](Formats_Material "wikilink") page for
details.

As was implied before, the texture(s) used by a model are not stored in
the md5mesh or md5anim files; they are specified by a separate shader
file that is placed in the `scripts/` directory.

    models/buildables/trapper
    {
        diffuseMap models/buildables/trapper/trapper.tga
        normalMap models/buildables/trapper/trapper_n.tga
        specularMap models/buildables/trapper/trapper_s.tga
    }

Do take note that `models/buildables/trapper` is NOT a path, it is
merely a string that matches the shader specified by the `.md5mesh`
file.

## Configuring the model

Aside from the textures used by a model, the scale, vertical position,
and bounding box size of the model must be specified. This is done with
a configuration file. These were formerly placed in
`overrides/buildables/` (for buildables) or `overrides/classes/` (for
player models), but are now placed in `configs/`.

### Player models

The configuration file may use the following keywords:

*Note: this list is incomplete*

- `headoffset `<var>`x`</var>` `<var>`y`</var>` `<var>`z`</var>
- `sex `<var>`gender`</var>
  Sets the gender of the model. Options are `f` for female or `n` for
  neuter. Any other character is interpreted as male.
- `fixedlegs`
- `fixedtorso`
- `firstTorsoBoneName`
- `footsteps`
  - `default`
  - `flesh`
  - `metal`
  - `splash`
  - `none`
- `lastTorsoBoneName`
- `torsoControlBoneName`
- `neckControlBoneName`
- `modelScale`

As an example:

    name        "Basilisk"
    model       level1
    modelScale  1.0
    skin        default
    shadowScale 1.0
    hud         alien_general_hud
    mins        -18 -18 -18
    maxs        18 18 18
    crouchMaxs  18 18 18
    deadMins    -18 -18 -4
    deadMaxs    18 18 4
    zOffset     0.0

### Weapons

The configuration file may use the following keywords:

- `weaponModel `<var>`path`</var>
- `weaponModel3rdPerson `<var>`path`</var>
- `idleSound `<var>`path`</var>
- `icon `<var>`path`</var> — The relative path to the icon that is
  displayed in the HUD for that weapon.
- `crosshair `<var>`path`</var>
- `disableIn3rdPerson`

After those keywords, one of the following keywords must be used,
followed by an opening curly brace (`{`), more commands, and a final
closing curly brace (`}`):

- `primary` (engine constant: `WPM_PRIMARY`)
- `secondary` (engine constant: `WPM_SECONDARY`)
- `tertiary` (engine constant: `WPM_TERTIARY`)

The configuration between the curly braces is handled by
`CG_ParseWeaponModeSection`, in the same file. It accepts the following
keywords:

- `missileModel `<var>`path`</var>
- `missileSprite `<var>`size`</var>` `<var>`shader`</var>
  - <var>size</var> — The size of the missile sprite. If this value is
    negative, it is made zero.
  - <var>shader</var> — The shader describing the missile sprite.
- `missileRotates`
- `missileAnimates `<var>`startFrame`</var>` `<var>`numFrames`</var>` `<var>`frameRate`</var>` `<var>`looping`</var>
- `missileParticleSystem `<var>`name`</var>
- `missileTrailSystem `<var>`name`</var>
- `muzzleParticleSystem `<var>`name`</var>
- `impactParticleSystem `<var>`name`</var>
- `impactMark `<var>`size`</var>` `<var>`shader`</var>
- `impactSound `<var>`index`</var>` `<var>`path`</var>
  - <var>index</var> — The index of the sound file, clamped to the range
    \[0,3\]; up to four impact sounds may be defined with this keyword.
  - <var>path</var> — The file path of the sound file to use.
- `impactFleshSound `<var>`index`</var>` `<var>`path`</var>
  - <var>index</var> — The index of the sound file, clamped to the range
    \[0,3\]; up to four impact sounds may be defined with this keyword.
  - <var>path</var> — The file path of the sound file to use.
- `alwaysImpact`
- `flashDLightColor `<var>`red`</var>` `<var>`green`</var>` `<var>`blue`</var>
  Specifies the color of the muzzle flash dynamic lighting.

  - <var>red</var> — The red color component as a floating point number
    in the range \[0,1\].
  - <var>green</var> — The green color component as a floating point
    number in the range \[0,1\].
  - <var>blue</var> — The blue color component as a floating point
    number in the range \[0,1\].
- `continuousFlash`
- `missileDlightColor `<var>`red`</var>` `<var>`green`</var>` `<var>`blue`</var>
  - <var>red</var> — The red color component as a floating point number
    in the range \[0,1\].
  - <var>green</var> — The green color component as a floating point
    number in the range \[0,1\].
  - <var>blue</var> — The blue color component as a floating point
    number in the range \[0,1\].
- `missileDlight `<var>`size`</var>
  - <var>size</var> — If this value is negative, it is made zero.
- `firingSound `<var>`path`</var>
- `missileSound `<var>`path`</var>
- `flashSound `<var>`index`</var>` `<var>`path`</var>
  - <var>index</var> — The index of the sound file, clamped to the range
    \[0,3\]; up to four impact sounds may be defined with this keyword.
  - <var>path</var> — The file path of the sound file to use.

As an example, this is the configuration for the chaingun
(`models/weapons/chaingun/weapon.cfg`):

    weaponModel       models/weapons/chaingun/chaingun.md3

    icon              icons/iconw_chaingun
    crosshair         48 gfx/2d/crosshair-chaingun_s

    primary
    {
      flashDlightColor      1.0 1.0 0.0
      flashSound            0 models/weapons/chaingun/flash0.wav
      flashSound            1 models/weapons/chaingun/flash1.wav
      flashSound            2 models/weapons/chaingun/flash2.wav
      flashSound            3 models/weapons/chaingun/flash3.wav

      impactMark            8 gfx/marks/bullet_mrk

      impactSound           0 models/weapons/chaingun/impact0.wav

      impactParticleSystem  models/weapons/rifle/impactPS
      muzzleParticleSystem  models/weapons/chaingun/muzzlePS
    }

### Buildables

The configuration file may use the following keywords:

- `model `<var>`index`</var>` `<var>`path`</var>
  - <var>index</var> Some models may actually have several different
    model files (not sure why); this argument specifies which. Clamped
    to the range \[0,3\] (which should actually be \[0,
    MAX_BUILDABLE_MODELS\]), which means that you may use as many as
    four models per buildable. This is only used by the machine gun
    turret, which is composed of different parts.
  - <var>path</var> The file path where the model file is located. Note
    that for MD5 models, an extension of `.md3` is still to be used; it
    will automatically be changed by the engine.
- `modelScale `<var>`scale`</var>
  Scales the model linearly.
- `mins `<var>`minX`</var>` `<var>`minY`</var>` `<var>`minZ`</var>
  The coordinates passed to this and `maxs` define the bounding box for
  the model that is used for collision. The bounding box is always
  aligned to the global coordinate axes regardless of the orientation of
  the model, which is something to keep in mind when defining these
  values. You will likely have to debug these values by enabling drawing
  the bounding boxes. Load a map in developer mode with `\devmap` and
  set `\cg_drawBBOX` to 1. The three arguments combined form the
  coordinate of one corner of the bounding box, and `maxs` the opposite
  corner.
- `maxs `<var>`minX`</var>` `<var>`minY`</var>` `<var>`minZ`</var>
  Defines the opposite corner of the AABB. (See above.)
- `zOffset `<var>`offset`</var>
  Sets the vertical offset of the model; in other words, how far off the
  ground it is.

  - <var>offset</var> The offset as a floating point (decimal) value.

As an example:

    model       0 models/buildables/trapper/trapper.md3
    modelScale  0.8
    mins        -15 -15 -15
    maxs        15 15 15
    zOffset     -15

Note that at present, you do not have to change the filename extension
of the model to match what it actually is; that is, if the model is
actually an md5, you may leave the extension as ".md3" and not
".md5mesh" or whatever.

## Directory overview

This section provides an overview of the subset of the directory
structure used by models; directories used for other purposes have been
omitted.

- `armor/` Location of configurations for the three armor types (i.e.,
  light, helmet, and battlesuit). You should not have to edit these.
- `configs/` Location of configuration files for various models.
  - `buildables/`
- `scripts/`
- `gfx/` Location of various 2d effect textures, such as those used for
  weapons.
  - *Subdirectories omitted for brevity*
- `models/`
  - `ammo/`
    - `tesla/` Contains a single image used for the tesla sparks. Not
      sure why it's located here.
  - `buildables/`
    - `acid_tube/` Acid tube
    - `arm/` Armory
    - `barricade/` Barricade
    - `booster/` Booster
    - `dcc/` Defense Computer
    - `eggpod/` Egg
    - `hive/` Hive
    - `hovel/` Hovel
    - `medistat/` Medistation
    - `mgturret/` Machinegun Turret
    - `overmind/` Overmind
    - `reactor/` Reactor
    - `telenode/` Telenode
    - `tesla/` Tesla generator
    - `trapper/` Trapper
  - `players/`
    - `builder/` Human builder model.
    - `human_base/` Unarmored human model. Also includes the jetpack and
      battery pack.
    - `human_bsuit/` Battlesuit model.
    - `level0/` Dretch.
    - `level1/` Basilisk and advanced basilisk. (The advanced basilisk
      uses the same model as the regular dragoon, but a different
      texture.)
    - `level2/` Marauder and advanced marauder. (Same as basilisk with
      regard to advanced model.)
    - `level3/` Dragoon and advanced dragoon. (Same as basilisk with
      regard to advanced model.)
    - `level4/` Tyrant.
  - `weapons/`
    - `abuild/` As there is no weapon model for the granger, the only
      thing in this directory is a config to hide the (nonexistant)
      weapon model in third person (a hack, I guess).
    - `abuildupg/` Advanced granger weapon. Same as above, except the
      config file specifies sounds for the attack sounds (which are also
      located in this directory).
    - `ackit/` Advanced construction kit.
    - `blaster/` Blaster.
    - `chaingun/` Chaingun.
    - `ckit/` Construction kit.
    - `flamer/` Flamethrower.
    - `grenade/` Grenade.
    - `hive/` Sprites, configuration file, and sound file for the hive.
    - `lcannon/` Lucifer cannon.
    - `level0/` Dretch configuration and attack sound file.
    - `level1/` Basilisk configuration and attack sound files (hit and
      miss).
    - `level1upg/` Advanced Basilisk configuration and added gas attack
      sound file.
    - `level2/` Marauder configuration and attack sound files (hit and
      miss).
    - `level2upg/` Advanced Marauder configuration and added electric
      attack sound file.
    - `level3/` Dragoon configuration and attack sound files (hit, miss,
      and pounce).
    - `level3upg/` Advanced Dragoon configuration and added barb sound
      files and model.
    - `level4/` Tyrant configuration and attack sound files (hit and
      miss).
    - `lgun/` Lasgun
    - `lockblob/`
    - `mdriver/` Mass Driver
    - `mgturret/` Machinegun turret ***FIXME: why does this show up
      twice?***
    - `prifle/` Plasma rifle
    - `psaw/` Painsaw
    - `rifle/` Rifle
    - `shells/`
    - `shotgun/` Shotgun
    - `teslagen/` Tesla generator ***FIXME: why does this show up
      twice?***
- `overrides/` Depreciated directory for model configuration files. Use
  `configs/` instead.
  - `buildables/` Depreceated location for buildable model configs.
  - `classes/` Depreceated location for character model configs.
- `scripts/` Location for shaders.

## Getting the model in game

There are two approaches to test your model in-game. The model and
related files may be in actual folders, or the engine can load them from
a `.pk3` (package) file, which is really just a zip-compressed archive
with the extension changed. The process for creating these archives is
discussed on the [packaging game data](packaging_game_data "wikilink")
page.

## Testing the model

Once you have the model exported, the shader and configuration written,
and everything packaged into a .pk3 file and in place, you are ready to
test.

### Testing externally

Rather than testing the exported model in-game, you may also test the
model with a stand-alone MD5 viewer. At present, there is a viewer for
Windows available
[here](http://www.katsbits.com/files/md5/modelviewer_0.93a.zip).

### Testing in game

See the [testing](testing "wikilink") page.

## Troubleshooting

### Old exporter

*Please be aware that there are numerous issues with the old exporter
and the newer versions of Blender. See [the troubleshooting
section](#All_or_part_of_the_mesh_appears_to_be_sucked_to_the_center "wikilink")
below for more information. It is strongly recommended that you use the
[new exporter](#New_exporter "wikilink") instead.*

#### Error while exporting from Blender

<table>
<tbody>
<tr class="odd">
<td><figure>
<img src="Md5_export_error_no_armature.png"
title="Image:Md5_export_error_no_armature.png" />
<figcaption>Image:Md5_export_error_no_armature.png</figcaption>
</figure></td>
<td style="vertical-align:top;"><p>This error displays when the selected
object does not have an armature modifier. Any object exported as an md5
needs bones, even if it is static. If you are unsure of how to create a
static object with md5, just add an armature, set the playback start and
end frame to 1, and add a location or rotation keyframe at frame
1.</p></td>
</tr>
<tr class="even">
<td><figure>
<img src="Md5_export_error_no_animation.png"
title="Image:Md5_export_error_no_animation.png" />
<figcaption>Image:Md5_export_error_no_animation.png</figcaption>
</figure></td>
<td style="vertical-align:top;"><p>This error displays when there are no
keyframes. Follow the abov instructions for exporting a static object
with md5.</p></td>
</tr>
<tr class="odd">
<td><figure>
<img src="Md5_export_error_no_material.png"
title="Image:Md5_export_error_no_material.png" />
<figcaption>Image:Md5_export_error_no_material.png</figcaption>
</figure></td>
<td style="vertical-align:top;"><p>This error displays when the object
does not have a material applied to it. This is required by the script,
even though it really does not affect the exported result.</p></td>
</tr>
<tr class="even">
<td></td>
<td></td>
</tr>
</tbody>
</table>

### Appearance problems in-game

#### All or part of the mesh appears to be sucked to the center

*Please note that as of 2012-02-27, the MD5 exporter does not work
properly in several more recent versions of Blender. Use Blender 2.59
until this is fixed. See [the MD5 exporter
thread](http://www.katsbits.com/smforum/index.php?topic=167.msg2135#msg2135)
for more information.*

This can happen for a number of reasons:

- There are vertices without weights.
  *Solution*: apply weights to vertices that do not have them. If those
  verts are not to be animated, weight them to a bone that does not
  move.
- You are using Blender 2.61 and you have bones that have animated
  positions.
  *Solution*: Use an earlier version of blender until this is fixed in
  the exporter.
- You are using Blender 2.62 and you have bones that are not located at
  the origin and do not have a parent or have animated positions.
  *Solution*: Again, use an earlier version of blender until this is
  fixed in the exporter.

### "R_LoadMD5: vertex %i requires more than %i weights on surface (%i) in model '%s'"

This error is displayed in the console in game when a vertex belongs to
too many groups.

You can use this script to check your model for this before exporting:

    # Copyright 2012 Nicholas De Cicco. <velociostrich@gmail.com>
    #
    # Licensed under the Apache License, Version 2.0 (the "License");
    # you may not use this file except in compliance with the License.
    # You may obtain a copy of the License at
    #
    #   http://www.apache.org/licenses/LICENSE-2.0
    #
    # Unless required by applicable law or agreed to in writing, software
    # distributed under the License is distributed on an "AS IS" BASIS,
    # WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    # See the License for the specific language governing permissions and
    # limitations under the License.

    import bpy, math
    from bpy.props import *

    MAX_GROUPS_PER_VERT = 4

    # Switch to object mode for vertex selection to work
    bpy.ops.object.mode_set(mode='OBJECT')

    for obj in bpy.context.selected_objects:
        # Check to see that the object is a mesh.
        if obj.type != 'MESH':
            continue

        # Select verts that belong to too many groups
        for vertex in obj.data.vertices:
            if len(vertex.groups) > MAX_GROUPS_PER_VERT:
                vertex.select = True
            else:
                vertex.select = False

    # Switch back to edit mode so the user can see any selected verts
    bpy.ops.object.mode_set(mode='EDIT')

#### Using the Script

1.  Select the mesh (or meshes) that you would like to check.
2.  Create a new text editor window and text data block.
3.  Copy and paste the script into the text editor.
4.  Click "Run Script".

Once the script has ran, the 3d view will switch to edit mode and any
offending vertices will be selected. A handy tip: clicking an individual
vertex will reveal which groups it is a member of in the properties
shelf.

<figure>
<img src="Properties_shelf_vertex_groups.png"
title="Properties_shelf_vertex_groups.png" />
<figcaption>Properties_shelf_vertex_groups.png</figcaption>
</figure>

## Resources

- [MD5 file format
  documentation](http://www.modwiki.net/wiki/MD5_%28file_format%29)
- [Tools for MD5 and other file
  formats](http://www.katsbits.com/tools/#)
- [Older versions of Blender](http://download.blender.org/release/)

[Category:Tutorials](Category:Tutorials "wikilink")
[Category:Modeling](Category:Modeling "wikilink")