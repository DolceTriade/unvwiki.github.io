---
title: Homepath
permalink: /Homepath/
---

The *homepath* is the user data directory for Unvanquished and the
Daemon engine.

## Default locations

## Configuration

The homepath can be set on the command line using the `-homepath`
option. You must use this if you want to run more than one instance of
Daemon concurrently (for example both a dedicated server and a client),
because there is a single-instance restriction: only one instance of the
Daemon engine can use a given homepath at a time.

## Homepath contents

In the root of the homepath may be found log files, the client's RSA
key, the console command history, and temporary .nexe files for the
currently running gamelogic modules. It may contain the following
subdirectories:

| Directory      | Purpose                                                                           |
|----------------|-----------------------------------------------------------------------------------|
| `base/`        | For Linux [launcher](launcher "wikilink") users, default install path for engine  |
| `condump/`     | Records of console output, saved with the `condump` command                       |
| `config/`      | Executable (via `/exec`) scripts of console commands, in particular `autogen.cfg` |
| `crashdump/`   | Crash dumps (see [Breakpad](Breakpad "wikilink"))                                 |
| `demos/`       | [Recordings of gameplay sessions](Tutorials_Demo_recording "wikilink")            |
| `game/`        | Readable and writable area for gamelogic                                          |
| `glsl/`        | GLSL shader cache                                                                 |
| `pkg/`         | Downloaded [DPK](Formats_DPK "wikilink") packages (maps, mods)                    |
| `screenshots/` | Screenshots                                                                       |
| `videos/`      | Videos made from [demos](Tutorials_Demo_recording "wikilink")                     |