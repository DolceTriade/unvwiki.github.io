---
title: Game locations
permalink: /Game_locations/
---

## When using the Unvanquished launcher

## When installed using Flatpak

When installed using Flatpak, the default user path is:

| Platform        | Default user directory (homepath)                                   |
|-----------------|---------------------------------------------------------------------|
| Linux (Flatpak) | `${HOME}/.var/app/net.unvanquished.Unvanquished/data/unvanquished/` |
|                 |                                                                     |

The system directorys follows a different layout and can be split and
stored in various places (as system install or user install). When
installed system-wide, here is the parent directory for the directory,
to be used as *engine path* (even if it's not the engine path) in tools
like [NetRadiant](Tools_NetRadiant "wikilink"):

## When using the Universal zip

When using [Universal zip](Universal_zip "wikilink"), the default system
paths are:

| Platform      | Default binary directory (libpath)                      |
|---------------|---------------------------------------------------------|
| Linux/Windows | <Extracted directory>                                   |
| macOS         | <Extracted directory>`/Unvanquished.app/Contents/MacOS` |
|               |                                                         |

The default user paths are the same as the launcher ones.