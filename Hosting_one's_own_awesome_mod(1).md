---
title: Hosting one's own awesome mod
permalink: /Hosting_one's_own_awesome_mod/
---

For now, it's only some notes and improvements may come later.

Building the dpk (additions to how to build mod):

- with 7zip:
  `cd mod-`<name>`_src.dpkdir; 7z -tzip -mx=9 a ../mod-`<name>`_`<version>`.dpk .`
- can simply depends on Unvanquished, the mod's content will be applied
  on top of Unvanquished's data

To host a mod, one needs two types of software servers on the host
machine:

- an HTTP server (https does NOT work)
- daemonded

Starting daemonded: `./daemonded -homepath server +exec server.cfg`

Unvanquished provides it's own `maprotation.cfg` file internally, which
is used by default by provided file
(`rotation1 { goto defaultRotation }`)

Things to change in `config/server.cfg`:

- `sv_hostname "my awesome server"`: name displayed on server list
- `g_motd "my awesome mod"`: what to display when people connect
- `sv_allowdownload 1`: must be 1, since people won't have your mod
  otherwise
- `sv_dl_maxRate "1000"`: seems pretty useless, related to UDP download,
  slow as hell anyway
- `sv_wwwBaseURL "example.com/unvanquished/pkg"`: where to find the
  files to download, do not put protocol
- `sv_wwwDownload "1"`: enable HTTP download (otherwise only slow UDP
  download will work)
- `sv_wwwFallbackURL "dl.unvanquished.net/pkg"`: where to find packages
  you don't provide, a rather good idea, don't you think?
- `set fs_extrapaks mod-awesome`: mods to load at startup, relative to
  pakpath (TODO: document), up to the first underscore (_), since text
  after is reserved to versioning and extension. Last version will
  (probably?) always be used.

Last but not least, place in `example.com/unvanquished/pkg`:

- the dpk files people will need
- a file named `PAKSERVER` containing the text
  `ALLOW_UNRESTRICTED_DOWNLOAD`, you can download a ready to use one
  [there](https://dl.unvanquished.net/pkg/PAKSERVER).