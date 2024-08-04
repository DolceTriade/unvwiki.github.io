---
title: Libpath
permalink: /Libpath/
---

The *libpath* is a path used by the Daemon engine when opening certain
resources. There is exactly one libpath. Normally, it is the same as the
directory containing the engine binary (see [Game
locations](Game_locations "wikilink")), but it can be customized with
the (rarely used) `-libpath` command line option.

The following resources are located using the libpath:

- The Breakpad support binary
- NaCl support binaries
- A gamelogic module, if the cvar `vm.[cs]game.type` is set to a nonzero
  value.

Additionally, the `pkg` subdirectory of the libpath is added as a pak
search path. But this is not required to exist.

Excluding the gamelogic, shared libraries (.so/.dll/.dylib) are always
located using the engine's actual path, as they are loaded automatically
by the operating system before the program even starts.