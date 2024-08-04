---
title: Tutorials Running Unvanquished from Git
permalink: /Tutorials/Running_Unvanquished_from_Git/
---

This guide assumes you do not want to install the git version of the
game system-wide, but instead just want to test it.

Unvanquished from git requires a small amount of setup work for the new
resources to properly register as a [package](Filesystem "wikilink").
It's also recommended you use a separate fs_homepath when running it
(detailed below) so that you don't ruin your current Unvanquished
configuration.

## Preliminary

Make sure you have already followed these steps first:

1.  Have the latest Unvanquished (normal) release installed, or the
    [resources
    handy](Compiling_the_source#Acquiring_the_Game_Files "wikilink")
2.  [Getting the source](Getting_the_source "wikilink")
3.  [Compiling the source](Compiling_the_source "wikilink")

## Setup

Assuming:

- You are familiar with the Unix terminal. Windows users will probably
  have to copy the *main* folder rather than symbolically link it.
- You compiled the source into a nice, neat /build folder

Assuming we are currently in the folder the git repository was cloned
into, things should look somewhat like this:

`$ ls `
`archlinux/`
`basepak.sh*`
**`build/`**`  `
`build-macosx-app.sh*`
`build-macosx-app-single.sh*`
`cmake/`
`CMakeLists.txt`
`COPYING.txt`
`debian/`
`download-pk3.sh*`
`download-pk3-torrent.sh*`
`external_deps/`
`GPL.txt`
`macosx/`
**`main/`**
`README.md`
`src/`
`tarball.sh*`
`update-version-number.sh*`

The 'main' folder contains the extra resources we need to make the game
think is in a package, but we have to do some setup in the 'build'
folder first

`$ cd build/`

Make a new 'homepath' for the game to store its belongings. An empty
directory will do. Inside of it we also need a folder for our packages:

`$ mkdir newhome`
`$ mkdir newhome/pkg`

Now make a symbolic link back to our *main* folder. Follow [package
naming](Filesystem "wikilink") guidelines and include a version, even if
it's just a token number:

`$ cd newhome/pkg/`
`$ ln -s ../../../main gitmain_1.pk3dir`

## Running the game

Make sure you are in your build folder: a *daemon* executable should
exist:

`$ ls`
`cgame-qvm-native.so*`
`CMakeCache.txt`
`CMakeFiles/`
`cmake_install.cmake`
**`daemon*`**
`daemonded*`
`daemon-tty*`
`game-nacl-native-dll.so*`
`game-nacl-native-exe*`
`game.pexe*`
`game-x86_64.nexe*`
`game-x86_64-stripped.nexe*`
`game-x86.nexe*`
`game-x86-stripped.nexe*`
`irt_core-x86_64.nexe`
`lcc/`
`libbase-source-libs.a`
`libengine-source-libs.a`
`libnacl-source-libs.a`
`Makefile`
`nacl_helper_bootstrap*`
`newhome/`
`sel_ldr*`
`src/`
`vm/`

First we need to make sure the game uses the libraries you have compiled
with the game:

`$ export LD_LIBRARY_PATH=$PWD`

Now we run the game. We need to tell the executable where all of its
resources are stored when we run it, as well as to use the package we
just setup

`$ ./daemon -pakpath (folder full of pkgs) -homepath (newhome we just setup) +set fs_extrapaks (new package we just setup)`

For example:

`$ ./daemon -pakpath /usr/share/unvanquished/pkg -homepath newhome +set fs_extrapaks gitmain `

Extra useful options can be found on [Running the
game](Running_the_game "wikilink").

## Using game packages from git

Each Unvanquished pak is a repository under
[UnvanquishedAssets](https://github.com/UnvanquishedAssets) whose name
ends with `_src.dpkdir`. See [Modifying paks](Modifying_paks "wikilink")
for information on working with them.

[Category:Tutorials](Category:Tutorials "wikilink")