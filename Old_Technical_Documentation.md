---
title: Old Technical Documentation
permalink: /Old/Technical_Documentation/
---

## About the Dæmon engine

The is part of the grand family of Quake engines, having started as an
heavily modified Quake3. It started with the big improvements to the
renderer made by XReal and ET:Xreal, then the Dæmon developers developed
it further, making it the most advanced open-source Quake-derived
engine.

- lineage picture

Originally it was being developed as the engine for the Unvanquished,
the succesor of Tremulous, a new release of Dæmon coming out every month
with the corresponding Unvanquished Alpha. Other games are currently
looking at using it as their engine.

The most important [features](Engine_Features "wikilink") are:

- A modern [renderer](Engine_Renderer "wikilink") with shadows, skeletal
  models and post-processing effectsoul
- [NaCl](Engine_NaCl "wikilink")-based [virtual
  machines](Engine_Virtual_Machines "wikilink") which allows C++ in the
  gamelogic
- A somewhat clean C++ codebase (vs. the mess of C we inherited)

While the Quake 3 engine has originally been released under the GPLv2,
we want to have Dæmon completely licensed under a 3-clause BSD which
means that new files should use that license and that rewrites of
subsystem should be made from scratch as much as possible;

## Getting started

Dæmon's master [source code](Engine_Source_Code "wikilink") has [its own
repository](https://github.com/DaemonEngine/Daemon) hosted on
[DæmonEngine](https://github.com/DaemonEngine/) organization on Github
but it's usually built as Unvanquished submodule. After
[building](Engine_Building "wikilink") the engine you will get three
executables:

- daemon, the graphical client that the players use
- daemon-tty, a command line client that can be used for development and
  server administration
- daemonded, the server

There are not usable on their own, without a game to run on top but if
you built it from, inside a game's repository you should be able to run
daemon to start the engine. The engine accepts a number of [command line
flags](Engine_Flags "wikilink") to specify in which directories it will
find the assets, as well as to set variables or run commands at startup.

## Architecture

Like Quake 3 our engine runs the gamelogic inside a [virtual
machine](Engine_Virtual_Machines "wikilink") so that by simply
connecting to a server and downloading some assets, a whole different
game can be played. However, because of the technology underlying them,
the virtual machines run in a different process than the engine and can
only communicate through IPC (InterProcess Communication) such as
sockets and shared memory. This forces some architectural choice like
having a command buffer for VM-engine communication, and is in stark
contrast to Quake 3 in which the gamelogic was run in an interpreter in
the engine process.

The client-server communication still follows the Quake 3 model of
buffering entity snapshots to be played on the client side and likewise
the [renderer](Engine_Renderer "wikilink") buffers all graphics commands
to process them on another core. All this buffering is explained in more
detail in the [architecture](Engine_Architecture "wikilink") page. It is
to be noted that since the gamelogic is in its own process, we can kill
it safely: non-fatal errors simply shut down the gamelogic and return to
the main menu.

The source code is arganized as follows:

- **CMakeList.txt**: build system main file
- **cmake**: additional build system files
- **external_deps**: binaries needed to compile and run the game,
  downloaded on the first compilation
- **libs**: external libraries
- **src**
  - **common**: source files compiled both in the gamelogic and the
    engine
    - **cm**: Quake 3's collision model or physics
    - **IPC**: InterProcess Communication library
    - **math**: our math library
  - **engine**
    - **audio**
    - **botlib**: pathfinding library for the bots
    - **client**: other files specific to the client-side engine
    - **framework**: utilities used by both the client-side and the
      server-side engine
    - **null**: noop interfaces for a number of subsystem
    - **qcommon**: like framework, but containing only legacy files
    - **renderer**: the biggest part of the engine
    - **server**: files specific to the client-side engine
    - **sys**: system support files that haven't been moved in framwork
      yet
  - **shared**: support code to be used in the gamelogic only

## Development workflow

- When changing the engine
- When developing the gamelogic
- When changing assets

## Coding inside Daemon

- Code in common
  - Command
  - Cvar
  - Filesystem
  - Log
  - Math
  - System
- IPC / writing a new syscall

## Other

- References
- Nacl