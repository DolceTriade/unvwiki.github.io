---
title: Tutorials Modifying paks
permalink: /Tutorials/Modifying_paks/
---

When working on changes to Unvanquished game paks, it is inconvenient to
work directly with the `.dpk` package file format (see
[DPK](Formats_DPK "wikilink")) used in production, since it is a
[Zip](https://en.wikipedia.org/wiki/ZIP_(file_format)) archive. Hence,
the supports the `.dpkdir` package directory format for working in the
native filesystem. This article details a couple of possible workflows
for development using a dpkdir.

## Method 0: Modifying the `unvanquished` package

If you are building the Unvanquished gamelogic, then it is easy to
modify the contents of the `unvanquished` package, which are stored in
the same Git repository as the source code. Suppose you have the code
checked out in the directory `stuff/Unvanquished`:

1.  Make your modifications to the package contents in
    `stuff/Unvanquished/pkg/unvanquished_src.dpkdir/`.
2.  Add the command line args `-pakpath stuff/Unvanquished/pkg` when
    starting Daemon.

In fact, if you are building gamelogic, it is better to always add the
pakpath option like this to ensure there are no hiccups due to an
out-of-sync `unvanquished` package (but see
[Compatibility](Compatibility "wikilink")).

## Method 1: Quick and dirty modifications to an existing zipped package

1.  Find the package you want to modify in the
    [pakpath](Filesystem#Pakpaths "wikilink"). Let's say it's
    `res-weapons` and the file is called `res-weapons_0.51.dpk`.
2.  Extract `res-weapons_0.51.dpk` into a folder named
    `res-weapons_src.dpkdir`. (`src` is a [version
    string](Filesystem#Naming "wikilink") which is arbitrary, but must
    be "greater" than `0.51`). `res-weapons_src.dpkdir` should be in the
    same directory as the original dpk.
3.  Make your modifications inside the dpkdir directory tree.
4.  Start/restart the game. A `/devmap` (map change) suffices—it is not
    necessary to restart the entire program.

A disadvantage of this method: it is easy to forget to delete the dpkdir
when you are done.

## Method 2: Working from a source Git repository

This section describes a workflow for working from source for a package
that has its own repository (likely something in
[UnvanquishedAssets](https://github.com/UnvanquishedAssets)).

1.  Check out the Git repository. E.g.
    `cd morestuff && git clone https://github.com/UnvanquishedAssets/res-weapons_src.dpkdir.git`.
2.  Make your modifications in the directory tree of the Git repository.
3.  Build assets. In general, the game may not be able to load assets in
    their source form. For example if you're modifying a map, you'll
    need to build it with NetRadiant. In the `res-weapons` example,
    there are some IQE models that must be converted to IQM so that the
    engine can load them. For Unvanquished releases,
    [Urcheon](Tools_Urcheon "wikilink") handles this part for all types
    of assets.
4.  Launch Unvanquished, specifying the *parent* directory of the
    repository as a pakpath. E.g. `./daemon -pakpath morestuff`.

## Rapid iteration

Once you have Daemon running with the right flags and filesystem cvars,
you should be able to test new sets of modifications without restarting
the whole program.

- Forcing a map change (e.g. with `/devmap`) is the most reliable way to
  ensure assets are reloaded as it performs a full filesystem reload. If
  you create or delete any files, this method MUST be preferred in order
  to update the file list.
- If you only modify files used by the cgame/client, you can use
  `/vid_restart` to restart only the client. This method is of interest
  because it preserves game state.
- If you only modify files used by the sgame, you can use `/restart` to
  restart only the server. This method is of interest because it is
  considerably faster.

## Tips

- Use the `which` command in the in-game console to verify that files
  are being loaded from your dpkdir:

`/which scripts/blaster.shader`
`File "scripts/blaster.shader" found in "C:\Users\slipher\Documents\My Games\Unvanquished\pkg/res-weapons_0.51.dpk"`

- In your operating system's settings you can associate the `.dpk` file
  extension with a zip archive browser such as 7-Zip to enable
  convenient inspection of paks ([DPK](Formats_DPK "wikilink") packages
  make use of Zip format).

<!-- -->

- If you want to [create a new
  package](Filesystem#Creating_your_own_package "wikilink") rather than
  modify an existing one, set the cvar `fs_extrapaks` to the package
  name. This forces your package to be loaded first, before
  `fs_basepak`.

[Category:Tutorials](Category:Tutorials "wikilink")
[Category:Mapping](Category:Mapping "wikilink")