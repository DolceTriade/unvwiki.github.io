---
title: Making an awesome mod
permalink: /Making_an_awesome_mod/
---

# Build the game

We start with an idea, like having grangers shoot rockets made out of
cake.

Apply the changes and [compile the
source](Compiling_the_source "wikilink").

Depending on the changes we need to build the client and server vms
(cgame and sgame).

# Package Manually

After building the game we have following needed files in the build
folder

`cgame-i686.nexe`
`cgame-amd64.nexe`
`cgame-armhf.exe`
`sgame-i686.nexe`
`sgame-amd64.nexe`
`sgame-armhf.nexe`

`cgame-i686-stripped.nexe`
`cgame-amd64-stripped.nexe`
`cgame-armhf-stripped.exe`
`sgame-i686-stripped.nexe`
`sgame-amd64-stripped.nexe`
`sgame-armhf-stripped.nexe`

Copy one of the sets and remove -stripped from the names if there.

Now create a text file named DEPS which contains

`unvanquished`

and place it in the same folder as your .nexe files

You can now place other assets in that folder to overwrite any original
files.

Keep the folder structure in mind. See the original assets for that

`unvanquished_src.dpkdir `[`https://github.com/UnvanquishedAssets/unvanquished_src.dpkdir`](https://github.com/UnvanquishedAssets/unvanquished_src.dpkdir)
`res-ambient_src.dpkdir `[`https://github.com/UnvanquishedAssets/res-ambient_src.dpkdir`](https://github.com/UnvanquishedAssets/res-ambient_src.dpkdir)
`res-buildables_src.dpkdir `[`https://github.com/UnvanquishedAssets/res-buildables_src.dpkdir`](https://github.com/UnvanquishedAssets/res-buildables_src.dpkdir)
`res-legacy_src.dpkdir `[`https://github.com/UnvanquishedAssets/res-legacy_src.dpkdir`](https://github.com/UnvanquishedAssets/res-legacy_src.dpkdir)
`res-players_src.dpkdir `[`https://github.com/UnvanquishedAssets/res-players_src.dpkdir`](https://github.com/UnvanquishedAssets/res-players_src.dpkdir)
`res-soundtrack_src.dpkdir `[`https://github.com/UnvanquishedAssets/res-soundtrack_src.dpkdir`](https://github.com/UnvanquishedAssets/res-soundtrack_src.dpkdir)
`res-voices_src.dpkdir `[`https://github.com/UnvanquishedAssets/res-voices_src.dpkdir`](https://github.com/UnvanquishedAssets/res-voices_src.dpkdir)
`res-weapons_src.dpkdir `[`https://github.com/UnvanquishedAssets/res-weapons_src.dpkdir`](https://github.com/UnvanquishedAssets/res-weapons_src.dpkdir)

Now zip the folder and rename it to

`mod-superawesomemod_0.0.1.dpk`

more naming infos at the [Packaging version
guidelines](Packaging_version_guidelines "wikilink")

# Run a Mod

Place your mod now into the pak folder

And when starting the game or server you use following command

`./daemon -set fs_extrapaks mod-superawesomemod`

The page [Hosting one's own awesome
mod](Hosting_one's_own_awesome_mod "wikilink") provide details on how to
host such server with downloadable files.