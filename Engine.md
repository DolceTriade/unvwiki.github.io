---
title: Engine
permalink: /Engine/
---

Unvanquished development uses the to power the , an ever-improving
engine with a long list of modern features (see below).

__TOC__

## Engine history

**Dæmon** can trace its lineage all the way back to Quake 3, integrating
the various features and improvements from quite a few engines before
it. The aim of Unvanquished Development is to make Dæmon the most modern
and best available quake-derived FOSS engine.

## Engine source code

The source tree is tracked on a dedicated repository to make
contributions easier and help projects to port their game on it:

- [Dæmon engine repository](https://github.com/DaemonEngine/Daeon)

## Engine features

### Sandboxed cross-platform virtual machine

The game code is sandboxed and running in a virtual machine.

For the virtual machine we currently use the [Native
Client](https://developer.chrome.com/docs/native-client/) (NaCl)
technology, and are in process to replace NaCl with
[WebAssembly](https://webassembly.org/) (Wasm) as industry shifted from
NaCl to Wasm.

The virtualized game code is cross-platform: build it once, deliver it
to players running on Windows, Linux and macOS. Once the engine runs on
a platform, the game code runs.

It makes very easy to modders to distribute their own game code to
players on supported operating system, and it makes very easy to players
to enjoy those mods since custom game code can be downloaded from
servers while running it sandboxed.

Unlike the old Q3VM technology we're not limited to the old C version
supported by the non-free LCC compiler, and we can use third-party C++
libraries in the game code, while running it with close-to-the-metal
performance in a sandboxed virtual machine.

### Rendering

- Modern OpenGL 3 renderer with very large hardware support,
  see the [GPU compatibility
  matrix](GPU_compatibility_matrix "wikilink");
- Improved Quake 3 shader (material) system:
  - Procedural vertex deformation;
  - Alpha mapping;
  - Specular mapping (color and intensity);
  - Physically based shading (PBR);
  - Normal mapping;
  - Relief mapping;
  - Glow mapping;
  - Multitextured terrain blending;
- Many special effects:
  - Motion blur;
  - Rim lighting;
  - Bloom;
  - Heat haze;
  - FXAA;
- Outline fonts;
- Procedural animation blending.

### Extensible virtual file system

See the and [Filesystem](Filesystem "wikilink") pages.

Game data is distributed as a set of DPK packages, which are Zip
archives storing files. Each file from each DPK packages is added to a
virtual file system that is seen by the game. The game code is only
allowed to explore that virtual file system (the game code is not
allowed to explore the user's file system).

This is very similar to the idSoftware PK3 and PK4 VFS but we extended
it to solve various design issues: unlike PK3 and PK4 a DPK can provide
a list of dependencies to load, so the game engine only loads the
required packages for the current game and for the map currently played
on.

The dependency mechanism also allows a package to extend an older
version of itself, either by adding files to the VFS, either by
replacing files from older packages, making possible for a game project
to deliver partial updates through light delta packages: with a suitable
distribution system (see our [updater/launcher](Launcher "wikilink")),
players would only download the delta paks containing the new files when
a new release is distributed.

### Networking

- Remote administration support;

- Custom `unv://` protocol to allow starting the game from a web browser
  or with an internet link;

-

### Miscellaneous

- Curses-based console

## Supported data formats

See [Filesystem](Filesystem "wikilink") for instructions on how to
package assets.

### Image formats

See the page.

- CRN — optimized for GPU (like DDS), ;
- WebP — lossy and lossless, for skyboxes as lossy, and lightmaps as
  lossless;
- DDS — Direct Draw Surface, optimized for GPU, **Well tested**;
- KTX — Khronos Texture, optimized for GPU, **Poorly tested**;
- PNG — lossless and slow, ;
- TGA — lossless but uncompressed, ;
- JPEG — lossy, .

### Material formats

See the page.

- Quake 3 materials;
- Dæmon materials — extension of Quake 3 materials with pre-collapsed
  stages and some features from Doom 3 and Xreal, including fixes for
  regressions from Doom 3 like multitextured multistage materials (like
  multitextured terrain blending);
- DarkPlaces materials — extension of Quake 3 materials with custom
  keywords (not all of them are supported) and implicit sidecar texture
  loading.

Other formats like and formats are not implemented in engine but in
Unvanquished game code.

### Sound file formats

See the page.

- Opus — lossy, ;
- OGG Vorbis — lossy, **Well tested**;
- Wav — lossless but uncompressed, .

### Model formats

See the , [Modeling](Modeling "wikilink") and pages.

- IQM — bone-based, ;
- MD5 — bone-based, **Well tested**;
- MD3 — vertex-based, .

### Map formats

See the and [Mapping](Mapping "wikilink") pages.

- Quake 3 / Wolf:ET style BSP (, ).

## Engine related blog posts

- [Announcing Dæmon engine Beta
  0.52](https://unvanquished.net/announcing-daemon-engine-beta-0-52/) by
  illwieckz;
- [Upgrading our 15-year-old
  engine](https://unvanquished.net/upgrading-our-15-year-old-engine/) by
  Kangz;
- [Merge of the first batch of engine-upgrade
  changes](https://unvanquished.net/first-engine-upgrade-merge/) by
  Kangz;
- [Big changes to the
  Filesystem](https://unvanquished.net/big-changes-to-the-filesystem/)
  by Kangz;
- [Moving the server-side gamelogic to
  PNaCl](https://unvanquished.net/moving-the-server-side-gamelogic-to-pnacl/)
  by Kangz.

# Non-engine features

## Game features

Some of those features were previously living in the engine, but we
moved them to the game code to make it easy to update them without
releasing the engine, and to simplify the interactions between engine
and game.

### Localization

Localization is implemented in Unvanquished game code, it supports
translation of C++ strings and RmlUI strings (starting with 0.53.0).

### RmlUi user interface

See the [UI](UI "wikilink") page.

The Unvanquished user interface is implemented using RmlUi (libRocket
before 0.53.0) supporting RML and RCSS formats based on HTML4 and CSS2
standards (it supports transforms!).

### Navigation meshes and bot behavior trees

See the and pages.

Unvanquished implements navigation mesh based bot AI configured with
behavior trees.

### Gameplay features

- [Voice say system](Voice_say_system "wikilink");
- Support for multiple [build layouts](Server_Map_layout "wikilink") per
  map.

## Game formats

### Particles and trails

See the and pages.

Unvanquished implements particle and trails, the formats are the ones of
Tremulous.

## Launcher and updater features

See the [Launcher](Launcher "wikilink") page.

### Auto updates

Our auto update mechanism is implemented as a game launcher. This is the
icon the player executes to run the game. The engine itself is just an
updatable file among others.

The launcher checks for updates at startup. If there is an update, the
update is downloaded and applied and the game is run. If there is no
update, the game is run.

### Peer-to-peer delta updates

The update is done using BitTorrent, enabling peer-to-peer download
(reducing pressure on game infrastructure) and partial updates (see
[\#Extensible virtual file
system](#Extensible_virtual_file_system "wikilink") on how the makes
possible to ship updates as delta packages).

### Configuration

The updater also does extra configuration steps like setting-up the
protocol (see [\#Networking](#Networking "wikilink")) to enable players
to join games by clicking links on web pages.

# Dæmon-based games

The is currently the only released game running on the .

Though, multiple projects are attempting to make games on or port games
to the .

See the [Daemon based games](Daemon_based_games "wikilink") page for
more information.