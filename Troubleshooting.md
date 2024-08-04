---
title: Troubleshooting
permalink: /Troubleshooting/
---

If you do not see your issue listed here, please seek support either on
the [support
forums](http://unvanquished.net/forum/forumdisplay.php/6-Troubleshooting)
or [chat](chat "wikilink"). If you think you may have found a bug,
please [report it](Bug_reporting "wikilink").

## All platforms

Before attempting any of the fixes listed here, you may want to [verify
your installation](Compiling_the_source#Verifying_the_Files "wikilink").
This takes minimal effort and corrupted asset files is often the
problem.

#### The game crashes with "recursive error 'Syscall ABI mismatch' after: Syscall ABI mismatch"

This is most of the time caused by having a wrong combination of assets
and executable. Try updating the game and assets.

### The console will not open

1.  Locate the autogen.cfg file in your profile folder, which is a
    subdirectory of your [data directory](#Data_directory "wikilink").
2.  Search for `"bind ~ toggleconsole"`, and delete the entire line, if
    present.
3.  Search for `"seta cl_consoleKeys"`, and ensure that `"~"` and
    `` "`" `` (at a minimum, though you may assign other keys if you so
    desire) are listed in a space-delimited quoted string. The line may
    look like this:
        seta cl_consoleKeys "~ ` 0x7e 0x60"

The console should now work by pressing the or keys.

### The game appears to stutter

Enable VSync either through the menu or by setting `r_swapInterval` to
`1`. Setting `r_swapInterval` to a value higher than `1` will
synchronize rendering to every *n*th refresh of the display; i.e., if
your monitor's refresh rate was 60 Hz, a value of `2` would result in a
framerate of 30 frames per second, a value of `3` would result in a
framerate of 20 frames per second, etc.

### Certain maps seem excessively bright

If maps appear far too bright (consistently bright with no static
shadows), your version of WebP is likely out of date. Get a newer copy
from Google and [re-compile](Compiling_the_source "wikilink").

### Trouble running the game on Unices after updating to Alpha 9

Make sure that you are running `daemon` and not `daemon.i386`; the name
has changed and you may safely delete the latter.

### The game crashes upon compiling shaders

[Run the
game](Running_the_game#Running_the_game_with_special_options "wikilink")
with "`+set r_recompileShaders 1`".

### Miscellaneous graphical anomalies

You may just need to recompile the shaders. Enter this at the in-game
console:

First, [take a screenshot](Taking_a_screenshot "wikilink") for a bug
report, then type this:

`/r_recompileShaders 1; glsl_restart`

If doing this fixed your issue, please open a bug report, include the
screenshot with the graphical anomaly and tell that command fixed the
bug for you.

If doing this did not fixed your issue, please open a bug report and
include the screenshot with the graphical anomaly.

### Not all servers are listed

Input the following into the in-game console:

`/reset protocol`

Hit the "Get New List" button in the in-game server browser, and the
formerly omitted servers should appear.

### menu list 'ui/menus.txt' not found, unable to continue!

The game files are not properly installed or they are corrupt. If this
is the case, make sure that the pk3s are in the `~/.Unvanquished/main`
folder, paying careful attention to spelling and capitalization.

## Linux

### Cracking Sound

In the options dialog which is reachable from the main menu set "OpenAL
Sound" to "No".

## macOS

### Mouse movement seems very slow

Input the following line into the console:

`/in_disablemacosxmouseaccel 0`

This will enable mouse acceleration.

## Windows

#### The game crashes with "recursive error 'Syscall ABI mismatch' after: Syscall ABI mismatch"

Run the game with the [special
option](Running_the_game#Running_the_game_with_special_options "wikilink")
`+set sv_pure 0`.