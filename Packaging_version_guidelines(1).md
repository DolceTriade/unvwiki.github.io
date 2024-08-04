---
title: Packaging version guidelines
permalink: /Packaging_version_guidelines/
---

# Naming conventions

Please follow these conventions when sharing your packages.

As a reminder, packages must be named this way:
<packagename>`_`<version>`.dpk`, and map packages **require** a special
`map-` prefix: `map-`<mapname>`_`<version>`.dpk`, <mapname> being the
basename of `maps/`<mapname>`.bsp` shipped in the `.dpk` package.

For more details about naming, see also the [DPK
Format](Formats_DPK "wikilink") page.

# Versioning conventions

## Recommended versioning schemes

According the the version algorithm implemented in the engine, version
strings *may* virtually use any character but the underscore one (`_`),
but you may want to avoid some versions schemes. This is because the
engine is not the only software tha will handle the package.

Let's imagine our map is named `castle`, here is an example of version
schemes that are known to be 100% safe.

First, start with a number, whatever it is (even `0` if you have no
better idea).

If you want to go the well-known `major.minor.patch` way, it's a good
choice. Note that trailing zeroes are useless:

- `map-castle_0.dpk`
- `map-castle_0.1.dpk`
- `map-castle_1.dpk`
- `map-castle_1.2.3.dpk`

If you do that, it's safe, but you don't have to:

- `map-castle_1.0.0.dpk`

You can increment the package for some updates without bumping the
version number by using the `+` (plus) character, like this:

- `map-castle_1.2.3+5.dpk`

This is useful when you repackage a package but it's still the same
version, for example when adding [navigation
meshes](Formats_Navigation_mesh "wikilink") that were missing, or
converting `png` images to `crn`, etc.

You can do complex things like this:

- `map-castle_1.2+20201231-2359-illwieckz.dpk`

In this case, this is a rebuild of the 1.2 version, done on December 31
of 2020 at 23:59 UTC by illwieckz.

This is recommended if you're not the usual author of the map. Server
owners needing to ship a fix to a map they host may want to do this,
just shipping the minor difference in that package, and relying on the
original package with the DPK dependency mechanism (here by setting
`map-castle 1.2` in the `DEPS` file).

You may want to use other schemes, like using a date. Keep in mind that
once you released a map with a version number scheme, the next releases
must use a greater version string.

It's also possible to do this:

- `map-castle_2020-01.dpk`
- `map-castle_2020-01-22.dpk`
- `map-castle_2020-01-22-1303.dpk`
- `map-castle_2020-04.dpk`
- `map-castle_2021.dpk`

But keep in mind that after that you will never be able to release
`map-castle_1.dpk` if the later reflects what you may call a “release
1”.

## Versioning schemes that are exotic but not that troublesome

Things like *alpha* and *beta* are not version numbers but labels, you
don't have to tell them in version number. If you really want to, the
only safe way is to put them **after** the version number, like this:

- `map-castle_0.1a.dpk`
- `map-castle_0.2.5a.dpk`
- `map-castle_0.3b.dpk`
- `map-castle_4b.dpk`

Better not put them before the version number (see below).

Note that third party tools like web servers and file browser may sort
`map-castle_0.2.5a.dpk` **after** `map-castle_0.2.5.1a.dpk`, leading
users to pick a file that they believe to be the most recent one because
being listed as the last one when sorted alphabetically, which is not
what you want. This is not a big issue because you can still issue a
greater version after that, like `map-castle_0.2.6.dpk`, and the
misleading will stop without much extra cost. So, this is troublesome,
but if one day you release `map-castle_0.1a.dpk` you wont suffer from
this for your entire life, while you would have to pay the bill for your
entire life if you release `map-castle_a1.dpk`.

## Sharing preview versions of standalone dpk files

In the past it was possible to use the tilde character (`~`) to
distribute preview package. In fact this is still 100% supported by the
game and the engine and we have no plan to remove that support. For
example after `map-castle_1.1` it was possible to distribute
`map-castle_1.2~20200101` before distributing `map-castle_1.2` because
the engine considers `1.2~20200101` is smaller than `1.2`, but because
of third party software we don't have control on (see below), please
don't do that anymore if you expect your users to download your files by
hand.

What you can do instead after having distributed `map-castle_1.1`, you
can distribute `map-castle_1.1-20200101` before distributing
`map-castle_1.2`.

## Special version schemes

Maps and other packages hosted in git repositories usually use the
special `src` and `test` version numbers. This is only used with
`.dpkdir` directories and must not be used with `.dpk` archives.

Usually, the layout is this one:

- `src/map-castle_src.dpk`
- `build/test/map-castle_test.dpk`
- `build/pkg/map-castle_1.2.dpk`

It is expected the `test` version string to be greater than `src`
version string in case you are loading by mistake both `src` and `test`
directories with the game, this ensures you test what you just built.

It is expected the `src` version string to be greater than `1.2` version
string in case the level editor loads both your game home path and your
source directory, this ensures you are loading assets from your source
directory and not from previously and older released packages.

## Version schemes to avoid

### Avoid version strings not starting with a number

It is **strongly discouraged** to distribute a `.dpk` package with a
version string starting with something that is not a number, for example
`src/map-castle_b3.dpk`.

This is discouraged because by doing that you close the door forever to
use some third-party versioning tools like Git or asset package build
tool relying on Git, and if you don't care for yourself, you close the
door for any contributor to your package or someone who may want to
maintain your package after you left the scene, like to fix issues or to
port your map or other packages to newer versions of the game or newer
version of the engine.

Tools built around git (like the GitHub forge, the Urcheon game package
builder…) expects version tag to be stored in repository as a string
starting with a `v` character followed by a number, then followed by
everything you want. For example for the `src/map-castle_1.3.dpk` map,
someone using git repositories will set the `v1.3` tag. Then third
party-tools may produce source archive automatically based on this tag,
or look-up this tag to automatically produce the
`src/map-castle_1.3.dpk` for yourself, even writing for you the `DEPS`
file with `castle 1.3` string for subsequent releases (incremental
build).

In the past in the Quake III Arena and Tremulous mapping scenes, it was
common to see maps named this way (for “alpha 1” and “beta 2”):

- `map-castle_a1.pk3`
- `map-castle_b2.pk3`

As we seen, this is a problem by itself because of third-party
source-management and build tools.

Then came the problem of `a1` and `b2` being greater than `1.0`, so both
“alpha 1” and “beta 2” being greater than “release 1”. To solve this
problem, some users did on of those to variants (for “release 1” or
“version 2”):

- `map-castle_r1.pk3`
- `map-castle_v1.pk3`

This have unwanted effects because if you go the `r1` way, your previous
`map-castle_r1.dpk` “release 1” would take precedence over your
`map-castle_src.dpkdir` source directory while you're editing your
upcoming “release 2”, the editor will not load your sources, but what is
meant to be obsolete!

If you do the `v1`, this is worst, your previous `map-castle_v1.dpk`
“version 1” would take precedence over both your `map-castle_src.dpkdir`
source directory *and* your `map-castle_test.dpkdir` build directory.
Both the level editor and the game will load obsolete assets when you
want to edit what must be your upcoming “version 2”.

### Avoid version strings containing a tilde character

You better not use the tilde character in your version string because
the Google Chrome web browser and derivatives (Chromium) automatically
rename files, replacing the tilde character (`~`) with the minus/hyphen
character (`-`) when downloading a file by hand from a web server.

This means that if you distribute a package named `map-castle_2~1.dpk`
in hope it will take precedence over your previous `map-castle_1.dpk`
release but will be obsoleted by your future `map-castle_2.dpk` release,
people downloading your map from a web server to host the map on their
own game server will get a file named `map-castle_2-1.dpk` instead,
already obsoleting your future, to-be-released, `map-castle_2.dpk`
package.

So the day you will release `map-castle_2.dpk`, the game server hoster
will download it, put it on his server, but the server will still play
the pre-release `map-castle_2-1.dpk` package instead!

Then, to fix that you would have to skip a number and go straight to
`map-castle_3.dpk`, meaning Google decided the version number of your
package, not you.

# Advices when porting maps from Tremulous or other games using methodologies from the 1999 era

When porting maps using problematic version numbers from an era `Git`
did not existed yet, you may want to follow this renaming scheme:

- `map-castle_a1.pk3` → `map-castle_0.0.1.dpk`
- `map-castle_alpha1.pk3` → `map-castle_0.0.1.dpk`
- `map-castle_b1.pk3` → `map-castle_0.1.dpk`
- `map-castle_beta1.pk3` → `map-castle_0.1.dpk`
- `map-castle_r1.pk3` → `map-castle_1.dpk`
- `map-castle_v1.pk3` → `map-castle_1.dpk`

Note that you are also free to do whatever you want, like:

- `map-castle_a1.pk3` → `map-castle_1.dpk`
- `map-castle_a1.pk3` → `map-castle_0.1.dpk`

Or start a new version cycle.

But if you port a map you're not the author, and so you did not decided
the version cycle at first, better do:

- `map-castle_a1.pk3` → `map-castle_0.0.1.dpk`

This way if the mapper comes back, he will be happy to still be able to
release a “version 1” of his precious map one day.

If in the past the map was named this way:

- `map-castle1.pk3`
- `map-castle2.pk3`

Or even:

- `map-castle1_1.0.pk3`
- `map-castle2_1.0.pk3`

You may want to just do name and versionnize this way:

- `map-castle_2.dpk`

Given the underscore (`_`) cannot be used in map name, if an old map
uses it in map name, you can replace it with a hyphen.

Note that you would have to rename the `.bsp` file accordingly, the
directory containing the external lightmaps (the directory containing
`lm_*.*` files) if exist, and the `q3map2_*.shader` file if exists, like
this:

- `magic_castle_a1.pk3` → `map-magic-castle_0.1.dpk`

With:

- `maps/magic_castle_a1.bsp` → `maps/magic-castle.bsp`
- `maps/magic_castle_a1/` → `maps/magic-castle/`
- `scripts/q3map2_magic_castle_a1.shader` →
  `scripts/q3map2_magic-castle.shader`

And replacing all occurrences of `maps/magic_castle_a1` to
`maps/magic-castle` in `scripts/q3map2_magic-castle.shader`.

Note that you may have other things to do while porting maps (especially
about level shot and things like that).