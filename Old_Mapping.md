---
title: Old Mapping
permalink: /Old/Mapping/
---

## Overview

Map geometry is created using either a conventional modeling program
(such as Blender) or with some variant of Radiant. Do note that if you
intend on using Blender, you will need to use Radiant to perform a few
final steps. This is discussed further below.

Radiant is the name used to refer to id Software's map editing tools
from Quake 3 onwards.

- QuakeEd — Developed internally at id and used to create maps for
  Quake. Written for NextStep.
- QE4 — Developed internally at id and used to create maps for Quake II.
- QERadiant — A fork of the released QE4 source code by Robert Duffy.
- Q3Radiant — id Software's fork of QERadiant used to create maps for
  Quake III. Windows-only.
- [GtkRadiant](http://icculus.org/gtkradiant/) — A port of Q3Radiant
  using the Gtk+ GUI toolkit, making it cross-platform (available to
  Linux and Mac OS X). Development stalled after 1.5 for a number of
  years, but has resumed with the recent release of version 1.6, which
  (for now) removes support for a number of games, including Tremulous.
- [NetRadiant](http://dev.alientrap.org/projects/show/netradiant) — A
  fork of GtkRadiant (?) by Alientrap, developers of the former (FOSS)
  Nexuiz project. The project page for this fork is currently down, but
  builds are still available from noted Tremulous mapper [Ingar's
  site](http://ingar.satgnu.net/gtkradiant/). The Xonotic project is
  currently maintaining NetRadiant; source code is available from [their
  site](git://git.xonotic.org/xonotic/xonotic.git) and is also
  [viewable](http://git.xonotic.org/?p=xonotic/netradiant.git).
- [DarkRadiant](http://darkradiant.sourceforge.net/) — A fork of
  GtkRadiant with the aim to improve the user interface and primarily
  intended to support Doom 3.
- [MacRadiant](http://www.redsaurus.net/00/node/4) — A port of
  GtkRadiant to Mac OS X.

### Map editor comparison matrix

This table provides a comparison of all modern map editing tools
available.

| Program                                                                                                                 | Supported OSes                |                     |
|-------------------------------------------------------------------------------------------------------------------------|-------------------------------|---------------------|
| Mac OS X                                                                                                                | Windows                       | Linux               |
| [NetRadiant](http://dev.alientrap.org/projects/show/netradiant) ([Ingar's builds](http://ingar.satgnu.net/gtkradiant/)) | 10.5, 10.6<sup>3</sup>        | Yes                 |
| [GtkRadiant](http://icculus.org/gtkradiant/)                                                                            | No                            | Yes                 |
| [DarkRadiant](http://darkradiant.sourceforge.net/)                                                                      | No                            | Yes (32 and 64-bit) |
| [MacRadiant](http://www.redsaurus.net/00/node/4)                                                                        | Yes<sup>2</sup> (Intel & PPC) | No                  |
| [QuArK](http://quark.sourceforge.net/)                                                                                  | No                            | Yes                 |
| [Gmax](#Gmax "wikilink")                                                                                                | No                            | Yes                 |
| [Blender](#Blender "wikilink")                                                                                          | Yes                           | Yes                 |
|                                                                                                                         |                               |                     |

1.  Binary packages are not yet available (but have been promised by the
    developer).
2.  Problems have been reported with Snow Leopard and Leopard, though
    there are workarounds. See the download page for more information.
3.  Binaries are for Intel systems only. Requires that X11 be installed.
    Users of 10.7 can get this from the [XQuartz
    project](http://xquartz.macosforge.org/landing/).

### Using other than Radiant to create maps

There are a handful of alternatives to Radiant for creating maps.

#### Miscellaneous

Note that these programs are not currently recommended for use.

- [Milkshape 3D](http://www.milkshape3d.com/) is an open source modeling
  program that reportedly has the ability to export in the `.map`
  format.
- [Qoole](http://www.volved.com/qsr/) is an editor for Quake 1 and 2
  maps.
- [TrenchBroom](http://kristianduske.com/trenchbroom/) is an editor for
  Quake 1 maps. The author has stated that they intend on adding support
  for Quake 3 in the future. TrenchBroom is notable in that it is *not*
  a derivative of Radiant and has an entirely unique UI.

#### Gmax

[Gmax](http://www.turbosquid.com/gmax) is a free variant of a very early
version of 3ds Max, roughly similar to version 3 or 4. As it was
intended to create mod content for games, it has a more restrictive
license agreement than a licensed copy of 3ds Max. Those games which are
supported by Gmax require the installation of the appropriate game pack;
there exists a [game pack for Quake
3](http://storage.turbosquid.com/Download/index.php?FuseAction=Download&ID=L567282&DLC=2M6F37BQVS)
that might make it possible to use Gmax to create maps for Unvanquished.
Do note that the legality of using Gmax to create content for games
other than Quake 3 [has been questioned in the
past](http://en.wikipedia.org/wiki/Gmax#Software_license_agreement).

#### Blender

While geometry other than triangles may be used during map creation, the
map compilation tools can only handle brush geometry; as of now, the
`.map` exporter for Blender can only convert polygonal geometry
(triangles) to brushes, and as such it would be pointless to use
anything else during the construction of a map except as a placeholder.

A comprehensive guide of using Blender to create map geometry ready for
Radiant and the compilation tools is available from
[katsbits](http://www.katsbits.com/tutorials/blender/map-basics-tutorial.php).

## Acquiring the game pack

To use any version of Radiant to create maps for Unvanquished, you will
need to download the associated game pack. Note that game packs for
NetRadiant and GtkRadiant differ in format, and as such cannot be used
for both applications without modification.

### GtkRadiant 1.4 & 1.5

Versions 1.4 and 1.5 of GtkRadiant included the game pack for Tremulous,
which can currently be used to develop for Unvanquished. **Not true
anymore.**

### GtkRadiant 1.6

Version 1.6 does not include the game pack. You must either extract the
game pack from Tremulous or acquire it from SVN:

`$ cd `<var>`/path/to/GtkRadiant`</var>`/installs`
`$ svn co `[`http://svn.icculus.org/gtkradiant-gamepacks/TremulousPack/trunk/`](http://svn.icculus.org/gtkradiant-gamepacks/TremulousPack/trunk/)

#### Installation

##### Windows

Place the game pack in the `installs/` subdirectory.

##### Linux

GtkRadiant 1.6 can read game packs from the `~/.radiant/1.6.2`
directory. Place the contents of the extracted archive there.

## Tutorials

- [Creating Your First
  Map](Mapping_Tutorials_Creating_Your_First_Map "wikilink")

## Design mentality

This section is oriented towards those with less experience mapping.

There are many potential pitfalls of map creation. Possibly the easiest
to fall into is spending too little time on design and spending too much
time on map details before even having a working base design. There is
an adage that applies well here: "Weeks of effort will save hours of
planning." Before you begin creating, do not concern yourself so much
with visual elements but the physical layout of the map.

A good strategy is to use placeholder textures (such as those containing
only text labels to identify what each finished surface should be, such
as "cement wall" or "window") and very basic geometry at first, then
playtest with as many people as possible as much as possible to evaluate
gameplay, making adjustments to the basic level geometry as necessary;
the emphasis during this phase of development is making many small
iterations to get feedback as fast as possible. Only when gameplay seems
stable would you then begin adding details.

When designing a map, consider the following:

- What can players use to help themselves navigate the map? What would
  make a good landmark or how can different areas of the map be
  differentiated visually?
- Is the map partitioned well visibly? Are there any areas that may
  cause poor performance?
- Are corridors large enough to facilitate combat?
- Does the map provide other good locations to build in aside the
  defaults?
- Is the map biased towards one side or another?

## Understanding Radiant

*This section is oriented at those who are new to Radiant who have not
used other, similar mapping tools such as those for Enemy Territory:
Quake Wars, Call of Duty, Valve's Hammer editor, and UnrealEd.*

The process for creating a map in Radiant is significantly different
than conventional polygonal modeling; instead of meshes, Radiant uses
<dfn>brushes</dfn> to define the space in which the player may occupy.
The fact that all brushes enclose a volume (unlike a mesh, which does
not necessarily have to) and the way in which brushes are used to
construct a map is referred to as <dfn>constructive solid
geometry</dfn>. Essentially, because brushes by definition enclose a
volume, they are said to be <dfn>solid</dfn>, and may be combined in
ways to produce more complex geometry. For example, a cut in one brush
may be made by subtracting the volume enclosed by another brush from it.

Those who have used UnrealEd may be familiar with the idea that the
entire world begins as a solid volume. The player naturally cannot move
in a solid, so before you can create rooms of a level, you must subtract
from that initial filled volume to create a void. From there, that void
can be filled with brushes that create walls and ceilings and floors (or
rocky mountains and terrain if you please; all brushes are created equal
and may be used for any purpose). This constitutes a level.

Radiant, however, models the world as a void, so no initial subtraction
is necessary. Rather, brushes must be added to create a level
<em>sealed</em> from the void; any gap allowing access into the void,
however small, is called a <dfn>leak</dfn> and will prevent you from
successfully [compiling](Mapping#Compilation "wikilink") your map.

Note that brush coordinates are <dfn>quantized</dfn>, which essentially
means that they must be aligned to a grid. Also, faces must constitute a
plane, so it can be difficult to move the vertices of a face into
position as Radiant will only allow new vertex positions that satisfy
this requirement, while at the same time restricting positions to those
that are on the grid.

## Using Radiant

Shortcuts for different versions of Radiant are the same unless
otherwise noted.

### Selecting brush geometry

- Press and hold <span class="hotkey">Shift</span> and click objects to
  select them (or deselect them if they are already selected).
- With nothing selected, press and hold
  <span class="hotkey">Shift</span> and click and drag to select
  multiple objects at once in a rectangle.

### Editing brush geometry

- Click and drag to create a new brush.
- With a brush selected, click and drag the mouse cursor to change the
  size of the selected brushes.
- Press <span class="hotkey">Esc</span> to deslect everything.

| Description   | Key       |
|---------------|-----------|
| Nudge Left    | Alt+Left  |
| Nudge Right   | Alt+Right |
| Nudge Up      | Alt+Up    |
| Nudge Down    | Alt+Down  |
| Edit edges    | E         |
| Edit vertices | V         |
| Edit faces    | F         |
|               |           |

### Placing entities

- Right-click in a 2d viewport to access the entity placement context
  menu. See "[Entities](Entities "wikilink")" for a discussion of what
  these are for and what is available.

### Linking entities

A target relationship can be established between two entities by
selecting them, then pressing .

### Navigating the views

#### Changing viewport layout

To change the layout of the viewports:

1.  Go to Edit → Preferences… or press <span class="hotkey">P</span>.
2.  In the preferences dialog, select "Layout" (under "Interface") from
    the left panel.
3.  Select your desired view layout.

Note that to see this change in effect requires restarting Radiant.

#### 3d viewport

- Scroll using the mouse wheel to dolly the camera forward or back.
- Right-click on the viewport to look around. Using the mouse wheel to
  dolly the camera works while in this mode.
- Press to move the camera up and to move the camera down. Note that
  this moves in finer increments when in free look mode.

#### 2d viewports

- Right-click and drag to move the views around.
- Press <span class="hotkey">Ins</span> to zoom out and
  <span class="hotkey">Del</span> to zoom in.
- Change the view with the toolbar button:

<figure>
<img src="gtkradiant_toolbar_change_views.png"
title="gtkradiant_toolbar_change_views.png" />
<figcaption>gtkradiant_toolbar_change_views.png</figcaption>
</figure>

## Entities

*For a listing of all entities, please see the [full
article](Entities "wikilink").*

The term <dfn>entity</dfn> with regard to Quake games and derivatives
(which Unvanquished counts itself among) refers to any of a class of
things:

- Players (including those controlled by AI; i.e., "bots")
- Buildables
- [Trains](Entities_func_train "wikilink")
- Static models

Note that some entities are not tangible, and although all entities have
a position, not all entities appear where they are placed or are even
positionally dependent at all. These other entities are:

- Camera positions (for spectators)
- Light flares
- Teleporters
- Harmful areas
- Target positions
- Timers
- Map information
- Portals

As a mapper, you have control over the starting location of entities.
Some entities, of course, move, and you have no control as to where they
might go.

At a minimum, you must place the following entities:

- — The initial position of the spectator camera.

- — The location of the camera for the Aliens' team while they are
  waiting to spawn.

- — The location of the camera for the Humans' team while they are
  waiting to spawn.

-

-

Without these entities, although you will be able to compile your map,
you will not be able to load it in the game; an error will be displayed.

Note that if you do not also place an [Overmind](Overmind "wikilink")
(), any alien buildings you have placed will explode after a short
amount of time. The same will occur for human buildings if you do not
place a [Reactor](Reactor "wikilink") ().

### Models

Both static and animated models are supported, using either the or
entities, respectively.

| Format             |                |            | Static? |
|--------------------|----------------|------------|---------|
| Name               | Extension      | Type       |         |
| MD3                | `.md3`         | Binary     | Yes     |
| ASCII Scene Export | `.ase`         | Text       | Yes     |
| Lightwave          | `.lwo`         | Binary     | Yes     |
| Wavefront          | `.obj`         | Text       | Yes     |
| 3Dstudio           | `.3ds`         | Binary     | Yes     |
| PicoTerrain        | `.picoterrain` | Text/Image | Yes     |
|                    |                |            |         |

#### PicoTerrain

PicoTerrain is a format evidently invented by
[ydnar](http://shaderlab.com/) back in the early 2000s. The only
information on the format is in a thread on the [Splash Damage
forums](http://forums.warchest.com/showthread.php/5283#post50099). It
uses two image files and a small text configuration file.

## Size Guidelines

Note that 32qu is approximately 1m.

Player sizes, in quake units (qu):

|              |                |
|--------------|----------------|
| Dretch       | 30<sup>3</sup> |
| Granger      | 40<sup>3</sup> |
| Adv Granger  | 40<sup>3</sup> |
| Basilisk     | 36<sup>3</sup> |
| Adv Basilisk | 42<sup>3</sup> |
| Marauder     | 46×46×36       |
| Adv Marauder | 50×50×40       |
| Dragoon      | 52×52×55       |
| Adv Dragoon  | 58×58×66       |
| Tyrant       | 64×64×92       |
| Human        | 30×30×56       |
| Crouching    | 30×30×40       |
| Battlesuit   | 30×30×72       |

Players will need an opening at least 1qu wider to fit through (possibly
2qu). In addition, player bounding boxes do not rotate, which means
diagonal corridors need to be wider. (Set `cg_drawBBox` to `1` while
in-game to see.)

Doorways should be a minimum of 128×128qu. Corridors should be a minimum
of 196qu wide, although it is possible to use a mix of 196qu and 128qu
(see Niveus for an example), and at most 512qu wide. Do not create
corridors more than 1280qu long without plenty of cover. Currently,
large open areas and underwater areas are very human biased.

Alien bases need cover to hide things behind, the entrances should be
128×128qu and should not be easily visible from outside other entrances.

## New Features

You may be interested in the list of [engine
features](Engine_features "wikilink").

- If you would like to support bots on your map, you must generate a
  [navigation mesh](Navigation_Meshes "wikilink").
- Additional shader functions (e.g., normal mapping) have been added;
  please see the [XReal shader
  manual](http://tremap.xtr3m.net/__Games/Xreal/Manual_Shader_1/ShaderManual.htm)
  for more information.

### Realtime lights

This applies only to the modern (GL3) renderer.

1.  Add a light entity.
2.  Add the key "noradiosity" to the light, and set the value to "1".

## Testing maps in-game

For testing purposes, it is most convenient to place your compiled
`.bsp` file in the `main/maps/` subdirectory of the [data
location](Running_the_game#Data_locations "wikilink") appropriate to
your system. Once you have done that, you can load your map with either
the `devmap` or `map` commands after setting `sv_pure` to 0. The former
allows using special commands made for developpers ("cheats") that make
it easier to test. Additional commands are discussed on the
[testing](testing "wikilink") page.

## Testing maps publicly

You may opt to use a Map Test Server to publicly test maps under
development. You can upload a map there as soon as you've
[packaged](Packaging_game_data "wikilink") it accordingly.

You might consider announcing the release of your map by creating a new
thread on the [Map Releases
subforum](http://unvanquished.net/forum/forumdisplay.php/33-Map-Releases).
On that forum is also [a helpful
guide](http://unvanquished.net/forum/showthread.php/498-How-to-give-useful-feedback)
to offering constructive criticism, which doubles as a checklist of
things for map makers to consider about their creation.

## Packaging maps for distribution

If you want to distribute your map to the world (either for testing or
as a final release), you'll have to create a
[package](Packaging_game_data "wikilink"). Such packages may be
distributed automatically via the server download feature or other
means.

## Resources

### Miscellaneous

- [Understanding Vis and Hint
  Brushes](http://tremmapping.pbworks.com/w/page/22453205/Understanding%20Vis%20and%20Hint%20Brushes)

### Q3Map2

- [Official homepage](http://q3map2.robotrenegade.com/) (Note: some
  links are outdated)
- [Documentation](http://en.wikibooks.org/wiki/Q3Map2)
- [Additional Documentation](http://shaderlab.com/q3map2/manual/)
- [Shader
  Manual](http://robotrenegade.com/q3map2/docs/shader_manual/contents.html)
- [Source
  Code](https://github.com/TTimo/GtkRadiant/tree/master/tools/quake3/q3map2)

### Quake Shaders

- [Quake 3 Shader
  Manual](http://q3map2.everyonelookbusy.net/shader_manual/) — Contains
  information not present in the XReal shader manual.
- [XReal Shader
  Manual](http://tremap.xtr3m.net/__Games/Xreal/Manual_Shader_1/ShaderManual.htm)
  — Contains information on new shaders added with XReal.

### Theory

- [Excerpts from The Hows and Whys of Level
  Design](http://www.hourences.com/the-hows-and-whys-of-level-design-examples/)
  — includes information on gameplay and lighting.
- Multiplayer Level Design In-Depth:
  - [Part 1: The Specific Constraints of Multiplayer Level
    Design](http://www.gamasutra.com/view/feature/1795/multiplayer_level_design_indepth_.php)
  - [Part 2: The Rules of Map
    Design](http://www.gamasutra.com/view/feature/1785/multiplayer_level_design_indepth_.php)
  - [Part 3: Technical Constraints and
    Accessibility](http://www.gamasutra.com/view/feature/1775/multiplayer_level_design_indepth_.php)

### Tutorial Sites & Communities

- [Custom Map Maker's
  Wiki](http://www.custommapmakers.org/wiki/index.php/Main_Page)
- [Xonotic mapping
  resources](http://dev.xonotic.org/projects/xonotic/wiki/Mapping)
- [Useful mapping links thread on Tremulous
  forums](http://tremulous.net/forum/index.php?topic=14411.0)
- [Netradiant mapping video tutorial
  series](http://www.youtube.com/playlist?list=PL0DDC60C4E3A6CC64) —
  Aimed at maping for AlienArena, but much of the information is the
  same.
- [Tremulous Mapping
  Guide](http://tremmapping.pbworks.com/w/page/22453172/FrontPage) by
  Ingar and Jex. Very complete.
  - [Starting Tremulous
    Mapping](http://tremmapping.pbworks.com/w/page/22453200/Starting%20Tremulous%20Mapping)

### Software

- [Ingar's NetRadiant builds](http://ingar.satgnu.net/gtkradiant/)
  - [Unvanquished game
    pack](http://ingar.satgnu.net/gtkradiant/files/gamepacks/UnvanquishedPack.zip)
- [Official GtkRadiant
  Manual](http://icculus.org/gtkradiant/documentation/q3radiant_manual/)
  (may be out of date)

[Category:Tutorials](Category:Tutorials "wikilink")
[Category:Mapping](Category:Mapping "wikilink")