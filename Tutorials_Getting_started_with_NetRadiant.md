---
title: Tutorials Getting started with NetRadiant
permalink: /Tutorials/Getting_started_with_NetRadiant/
---

## Getting and installing NetRadiant

- Download a prebuilt archive from the [NetRadiant download
  page](https://netradiant.gitlab.io/page/download/).

<!-- -->

- Just unzip the archive and run the binary.

Arch Linux users can also use the
[netradiant-git](https://aur.archlinux.org/packages/netradiant-git)
PKGBUILD to get the editor.

## Gamepack

NetRadiant is designed to work with many Quake-based games, not just
Unvanquished. The Unvanquished gamepack is provided with NetRadiant so
you have nothing more to do. Just make sure the current game selected
for mapping in NetRadiant is Unvanquished.

## Start up NetRadiant for the first time

When you first start up NetRadiant you will be asked what game you want
to edit levels for.

- If Unvanquished is not listed, then you don't have the right
  NetRadiant package.
- If you don't want to see this dialog on startup you can untick the
  second checkbox.

<figure>
<img src="NetRadiant_global_preferences.png"
title="File:NetRadiant global preferences.png" />
<figcaption><a href="File:NetRadiant">File:NetRadiant</a> global
preferences.png</figcaption>
</figure>

You may also be asked for the game's *engine path* if NetRadiant can't
find it. This is the "default binary directory" in the table below. This
is the location where the game stores its folder holding the many
resources.

<figure>
<img src="NetRadiant_engine_path_not_found.png"
title="File:NetRadiant engine path not found.png" />
<figcaption><a href="File:NetRadiant">File:NetRadiant</a> engine path
not found.png</figcaption>
</figure>

Finally you should be greeted by NetRadiant's default interface:

<figure>
<img src="NetRadiant_main_window_default_layout.png"
title="File:NetRadiant main window default layout.png" />
<figcaption><a href="File:NetRadiant">File:NetRadiant</a> main window
default layout.png</figcaption>
</figure>

Make sure you have a *common* shader category. If you do not, contact
the devs via [chat](chat "wikilink") or the .

## Setting some recommended options

- Main window, menu *Edit \> Preferences*, tab *Settings*, **disable**
  *Add entity and brush number comments on map write*.
- Main window, menu *Edit \> Preferences*, tab *Settings/Brush*,
  **enable** *Always use caulk for new brushes*.
- Main window, menu *Edit \> Preferences*, tab *Interface/Layout*,
  **select** the layout with three 2D view and texture browser, the one
  on the absolute right in NetRadiant preferences.
- Texture browser, menu *View*, **enable** *Shaders Only*.

## Getting started

This is not a complete guide. Another tutorial will be required to tell
how to make a complete map with required entities and all, but if you
already mapped for other games before, this will give you the
prerequisites you may miss.

### Editing an existing map

Let's imagine you want to edit the map :

- Locate the file in your installation directory (see above) and extract
  it as in your user directory (see above). The file is a zip file with
  a different extension, so if your system does not recognize it, just
  make a copy with a extension and extract it.
- In the end you'll get something that looks like (and other files in
  the dpkdir). Just open that file in NetRadiant and do some edits, then
  build the map using the build menu. Congratulation, you can now load
  your edited map in game!

### Making a new map from scratch

Let's imagine you want to make a map named :

- Create a folder in your user directory (see above) in a way it is
  named .
- Create a subfolder named this way: .
- Add a file named this way: . For a start, just write in this file.
- Open NetRadiant, save the default empty file as .
- Click the refresh button on the toolbar, all the texture sets must
  appear in the texture browser! Now you can start mapping.

### Becoming a mapper

See [Mapping guide](Tutorials_Mapping_guide "wikilink").

[Category:Tutorials](Category:Tutorials "wikilink")
[Category:Mapping](Category:Mapping "wikilink")