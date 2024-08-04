---
title: Breakpad
permalink: /Breakpad/
---

Breakpad is the technology for generating and analyzing crash dumps for
the Daemon engine and NaCl gamelogic modules. A crash dump is a file
that is generated when the program crashes, which can be analyzed by
developers to find out why the crash occurred. Breakpad is currently
available in Daemon for the Windows (if built with MinGW) and Linux
engine code, and the NaCl gamelogic on any platform.

## Configuration

The USE_BREAKPAD CMake option controls whether Breakpad support is built
into the engine. It is disabled by default because Breakpad is primarily
useful for publicly distributed release binaries, not people who build
and run the code themselves. Note that NaCl crash dump support is always
built in, regardless of options.

For an engine built with Breakpad support, the `common.breakpad.enabled`
cvar turns it on or off. The cvar can only be set via the command line,
like `./daemon -set common.breakpad.enabled 0`.

## For users: reporting a crash

The crash dumps are stored in the homepath under the `crashdump/`
directory. Sort by date to find the most recent one and make sure it
matches the date/time when the crash occurred. Send the .dmp file to
someone on the Unvanquished development team.

## For developers: how to trace a crash

### 1. Getting the tools

The Breakpad repo for Daemon Engine is at
<https://github.com/DaemonEngine/breakpad>. If you have already checked
out Daemon, then it is located in the `libs/breakpad/` submodule there.
cd into this repo.

Daemon's Breakpad fork is based on
<https://github.com/jon-turney/google-breakpad>, with only minor
changes. Jon Turney's version adds MinGW support. It is in turn a fork
of Chromium's Breakpad
<https://chromium.googlesource.com/breakpad/breakpad>.

### 2. Get symbols

#### 2a. Symbols for an official Unvanquished release

If you are debugging an official release binary, you don't need to (and
can't) generate symbols yourself -- the Unvanquished release script
handles this. In the Unvanquished unizip/torrent (or updater
installation directory), symbol files are found in the
`symbols_${VERSION}.zip` archive. Simply extract the zip somewhere.

#### 2b. Generating your own symbols

To produce symbols, you need a binary with debug info. For MinGW, the
binary additionally needs to have been built with the flag so that it
has a nonzero build ID.

The first step is to build the dump_syms and/or dump_syms_dwarf
executable using Make. Then you can use the `symbolize.py` script in the
root of Daemon's Breakpad repository to produce the symbols and store
them in a symbol directory. Or if you want to know how to do it
yourself, you can read the following paragraph which describes what the
script does:

You need to run the dump_syms tool (located at
`src/tools/linux/dump_syms/dump_syms` for Linux or NaCl targets or
`src/tools/windows/dump_syms_dwarf/dump_syms` for MinGW targets) on the
binary(ies) where the crash occurred. Usage: `dump_syms `<binary>. The
output must be stored in a specific directory format. Pick a directory
to be the symbol directory (`symbols` in the following examples). The
output must be stored at `symbols/$FILENAME/$BUILD_ID/$FILENAME.sym` .
For example,
`symbols/cgame-native-dll.dll/1A74E057938E0BF10930C4F54740B2E21/cgame-native-dll.dll.sym`.
The build ID can be seen in the first few lines of dump_syms output in a
line beginning with `MODULE`.

### 3. Stack walk

Running the stack walk tool (located at
`src/processor/minidump_stackwalk`) will give the human-readable stack
trace. Usage: `minidump_stackwalk `<dump file>` `<symbol directory>.