---
title: Testing
permalink: /Testing/
---

## Reporting bugs

Please see the [bug reporting](Bug_reporting "wikilink") page. This page
is about helping modders and developers testing their changes.

## Debugging

To create a debug build, change `CMAKE_BUILD_TYPE` in CMake from
`Release` to `Debug`, then [compile](Compiling_the_source "wikilink").

You may find it necessary to set `in_nograb` to `1` to disable pointer
grabbing so that you may use your debugger.

### Debugging with gdb

Start gdb as follows:

`$ gdb --args ./daemon +devmap chasm`

If the program segfaults, a backtrace is very useful to the developers
in determining the source of the problem. At the debugger prompt, type
`bt`:

`(gdb) bt`

### Debugging with Xcode

With Xcode 4, even if you did not build the game with Xcode, you may
still use its facilities for debugging.

1.  Open any project. If necessary, create a new one. It may contain
    anything.
2.  Click "Product" on the menu bar and navigate to "Attach to Process".
    Look for "daemon" listed under "Applications".

After a moment, the application will be ready for debugging.

See the [Xcode 4 User
Guide](https://developer.apple.com/library/mac/#documentation/ToolsLanguages/Conceptual/Xcode4UserGuide/060-Debug_Your_App/debug_app.html#//apple_ref/doc/uid/TP40010215-CH3-SW1)
for more information.

## Live Testing

### Starting a testing session

Start the game, and enter the following command:

`/devmap `<var>`map-name`</var>

### Adding bots

Like fish in a fish bowl, they can bring some activity in a map.

`/bot fill 5   # add 5 bots`

You can also have a look at all the `g_bot_*` cvars, they are quite
interesting. There is even a graphical user interface for these!

### Moving around with ease and spawning anywhere

You can pass through walls and fly around using `/noclip`, and you can
spawn anywhere you want using `/devteam h` for humans or `/teamteam a`
for aliens. That's very practical and can allow you to start from an
empty map.

To load an empty map without having the game finishing immediately, you
can use `g_neverEnd`. This can help porting maps.

### The `/give` command

The /give will give you an easy way to test situations without being
blocked by funds or team advancement.

`/team a           # join aliens`
`/give momentum    # give all the momentum you can to your team`
`/give bp 100      # get 100 build points free`
`/give funds       # get rich quick! I swear it's not a pyramid scheme!`
`/give all         # get all personal things you can get, in addition to money (BP and momentum are independant)`

You can also combine several commands into one, for example you can test
advanced dragoon really quickly

### Some misc useful cvars

- `cg_drawSpeed` to see how fast you are moving, `/set cg_drawSpeed 2`
  even brings an histogram.
- `cg_drawBBOX` to see how big or small the bounding box are
- `cg_drawDebugDistance` to give you an idea of how far away of you a
  distance of "100 quake units" is
- `timescale` setting this will make everything faster, or slower. Be
  careful that if you set it too low (say less than 0.1) the graphical
  console will take a lot of time to visibly appear, but you can still
  type in it. For example to do `/timescale 1` again.
- `g_freeFundPeriod` to change how often you and other clients are
  gifted money. This can be an alternative to making bots ignore limits
  that can give a bit more diversity in their choices and behaviours
  (rich bots will always rush, for example)

## Debugging Graphics

- `cg_draw2D` can allow you to disable 2D drawing. It may be useful if
  you want to ignore 2D performances from your benchmarks.

There probably exist proprietary tools for your platform. For example
AMD used to have gDEBugger, and [GPU
PerfStudio](https://gpuopen.com/archived/gpu-perfstudio/) proprietary
debuggers.

### apitrace

[apitrace](https://apitrace.github.io/) is an open-source tool that
records every graphics API call made by an application. After the
application has closed, you can step through individual calls to the
graphics API, allowing you to

- see the result exactly as it would appear following each call,
- see graphs of API usage, and
- inspect buffers.

Linux users can install it from their package manager, for example:

`sudo apt install apitrace-tracers apitrace-gui`

Windows users can [download a
build](http://people.freedesktop.org/~jrfonseca/apitrace/).

## General Tips

### Miscellaneous

- To stress test the engine's ability to display a large number of
  buildables, you can tweak `g_BPInitialBudget` and build as much as you
  wish.
- To determine what file was loaded for a particular asset (e.g., to
  determine if files are being read from a particular archive) use the
  `/which` command with the relative path to the asset as an argument.
  You can use tab-completion.

For example, this means that you are effectively the new version of an
UI file:

`/which ui/shared/circlemenu.rcss`
`File "ui/shared/circlemenu.rcss" found in "/home/me/unv/Unvanquished/pkg/unvanquished_src.dpkdir/" `

## Viewing Runtime Information

The engine and game logic provide a number of commands for viewing
information about its current state.

## Testing materials and textures

See .

## Testing maps

See .

## Testing models

See .

[Category:Testing](Category:Testing "wikilink")