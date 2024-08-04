---
title: Daemon based games
permalink: /Daemon_based_games/
---

**[Dæmon](Engine "wikilink")** is the game engine powering Unvanquished.
The is a fork of the **XreaL engine** through the **ET:XreaL** variant
which derivates from both **Quake 3 engine** and **Wolfenstein: Enemy
Territory engine**.

- repository: <https://github.com/DaemonEngine/Daemon>

## Released games

### Unvanquished

**Type:** port.
**Status:** active, released (beta builds).

**[Unvanquished](Game "wikilink")** is the game maintaining the , first
release happened on February 29, 2012 and is still releasing new
versions 10 years later. Unvanquished derivates from the Tremulous game
that was initially released as a standalone game on an engine derivated
from ioquake3 in 2006, after having been a Quake 3 total conversion mod
for some time.

- Website: <https://unvanquished.net>
- Game code repositories: <https://github.com/Unvanquished>
- Game data repositories: <https://github.com/UnvanquishedAssets>

## Unreleased projects

### FreeFort

**Type:** remake.
**Status:** stalled.

- Website: <https://freefortgame.net>
- Repositories: <https://git.freefortgame.net/FreeFort>

**FreeFort** is the most recent attempt to make a game based on the and
the Unvanquished game code. The project is to remake a Team Fortress
2-like game as a fully free and libre open source game. The project is
in it's very early state and nothing is released yet.

The project is currently stopped.

### Unnamed project

**Type:** new game.
**Status:** unknown.

There is also another project whose name is not known yet and status
unknown to make a new game from scratch based on the (without reusing
the Unvanquished game code) which is more about being an infantry war
game. Few information is know about it. While doing this effort, [The
White Lion](Special:Contributions_The_White_Lion "wikilink") produced a
lot of very useful documentation in the [Technical
Documentation](Technical_Documentation "wikilink") page, especially the
*Program Ignition and Initialization* part and many other parts like
*Source Code Filesystem Tree Structure* or *System Architecture*.

The project is probably active but very few information is known about
it.

### UnrealArena

**Type:** new game.
**Status:** stalled, unreleased (as a playable game).

- Website: <http://www.unrealarena.net>
- Repositories: <https://github.com/unrealarena>

The project is currently stalled if the project managed to produce
multiple build, there is nothing playable.

**Unreal Arena** is a brand new game project (not a port) based on Dæmon
and Unvanquished code. The purpose is to provide the user two different
teams, one using Quake III Arena movements and weapons, another one
using Unreal Tournament movements and weapons, and let people frag
together.

The project managed to recreate a Quake 3 map (untextured) from scratch
and publish some alpha build just making possible for a tester to load a
map, join and navigate.

### Smokin' Guns

**Type:** port.
**Status:** dormant, unreleased (on ).

- Website: <https://www.smokin-guns.org>
- Repositories: <https://github.com/smokin-guns>

The project is currently dormant as most people involved are very busy
on other projects and other things in their life. Players should use the
ioquake3-based game for now.

This is a project to port the **Smokin' Guns game** to the . The Smokin'
Guns game already exist as a released standalone game running on
ioquake3 engine, it derivates from the Western Quake 3 total conversion
mod.

The project is to use the upstream (or to upstream the changes) and to
rebase the specific Smokin' Guns game mechanics on the Unvanquished game
to be able to merge improvements from Unvanquished as time passes.

Some fixes for Smokin' Guns assets were upstreamed to the , and a some
testing assets were produced to load Smokin' Guns maps with the
Unvanquished game and the for testing purpose and to fix related issues.

### Xonotic

**Type:** port.
**Status:** stalled, unreleased (on ).

- Website: <https://xonotic.org>
- Repositories: <https://gitlab.com/xonotic>
- Repository for the Q1VM glue:
  <https://gitlab.com/xonotic/daemon-glue/>

The project is currently stalled as all people involved in those various
attempts became busy with other things in their life. Players should use
the DarkPlaces-based game for now.

There was multiple attempts to port the **Xonotic game** on the .
Historically, Xonotic is running on the DarkPlaces engine. Xonotic as a
released standalone game running on the DarkPlaces engine exists since
September 8 2011 and is a fork (and continuation) of the defunct Nexuiz
game initially released on May 31, 2005.

The Darkplaces engine development was stalled and it was considered
difficult to improve it for non-technical reasons because the DarkPlaces
engine tries to keep compatibility with original Quake game and some
improvements wanted for the need of Xonotic may break compatibility.

On the other hand the can break things for the best (like fixing design
issues) and was seen as a live project. Multiple people from Team
Xonotic expressed the will to port their game on the .

The project was to port the Xonotic game code on the (not rebasing on
Unvanquished game code).

Such effort is not a an easy task because the is an engine derivating
from Quake 3 engine while DarkPlaces engine derivates from Quake (the
first) engine. Anyway, DarkPlaces already supports Quake 3 bsp files
(map format) and most of Quake 3 shaders (material format) which are the
ones natively supported by the , and Xonotic already uses those Quake 3
formats.

The difficulty is that the Xonotic game code is written in QuakeC and is
expected to run on a Q1VM, while Dæmon executes native code (currently
sandboxed in NativeClient) compiled from generic languages like C or
C++. There was multiple attempts to achieve the port, some people worked
on source transpilers to convert the QuakeC code base to less exotic
languages like C++ or Rust, others worked on writing a Q1VM expected to
run on the Dæmon virtual machine.

There was interesting progresses achieved by those various attempts, the
team managed to produce a minimalistic Q1VM running some minimal QuakeC
code base allowing to start the , load a map and walk around.

Xonotic developers helped to split the and the Unvanquished game,
developped some code to make the engine more standalone.

Lots of features were implemented in the Dæmon renderer using Xonotic
data files (maps, materials, textures…), for example the relief mapping
feature was debugged and fixed using Xonotic maps and materials, or the
ability to support both lose normal maps and normal maps embedded in
height maps was implemented. Also a lot of rewrite was done to make the
better and even helped Dæmon team to better understand some things to
make the engine better, for example the multitextured material blending
feature is a direct consequences from that, or the ability to support
multiple formats of normal maps.

The now provides some cvars to enable compatibility code to better
support medias purposed for the DarkPlaces engine.

This project also helped the Dæmon game engine to support both the newer
DPK format and the legacy PK3 format at the same time, because Xonotic
through Nexuiz has more than 15 years of history and there are thousands
of maps out there so porting maps was not really an option.

Xonotic data files (maps, materials, textures…) are still used today as
test bed for the to test for regressions and to implement new features:
Xonotic assets makes use of more rendering features than Unvanquished!
For example the Xonotic assets may be used to test the sRGB lightmap
technology we still need to implement.

The Xonotic and Unvanquished teams became very close, and multiple
Xonotic contributors also became Dæmon and/or Unvanquished contributors
(TimePath, Mario, Melanosuchus, EACFreddy…), making the engine better,
implementing features, etc. Some Unvanquished contibutors also started
to help Xonotic as we still have common interests. For example
Unvanquished contributors help Team Xonotic to maintain the
[NetRadiant](Tools_NetRadiant "wikilink") level editor which is also the
recommended level editor for Unvanquished.

## Special mentions (not Dæmon-based but very close)

### KingpinQ3

**Type:** remake (on a custom XreaL port).
**Status:** active, released (beta builds).

This project is *not* running on the but on another fork of **XreaL**
(like Dæmon), so technically both engines are very close and we share
common interests. For example hypov8 from KingpinQ3 converted our new
lasgun first person model to a usable third person model in
Unvanquished!

**KingpinQ3** is a remake of Xatrix Entertainment's **Kingpin - Life of
Crime game** on an engine derivated from Quake 3 through the **XreaL**
lineage like us!

- Website: <https://www.kingpinq3.com>
- Downloads:
  <https://www.kingpin.info/download/index.php?dir=other/standalonegames/KingpinQ3/>