---
title: Compatibility
permalink: /Compatibility/
---

# Inter-module compatibility

Unvanquished has many software components: engine binaries, based on the
Daemon repository (client and server); gamelogic binaries, based on the
Unvanquished repository (cgame and sgame); and various other files
shipped in DPKs, which may be used by any of the binaries. Currently,
all components are on a single release cycle. A given user normally has
only one version of the client installed, but different servers may
distribute differing versions of the other components via the
auto-download mechanism. This means many different combinations of
versions of the components are possible. It can be difficult to reason
about which combinations will work correctly, and even which
combinations ought to be allowed.

In the rest of this article, "Unvanquished" refers to the eponymous Git
repository, not the game.

## Desired use cases

### Use cases we want to support

- <b>Develop on next-release branch (e.g. `0.52.0/sync`) of all repos
  (Daemon, Unvanquished)</b>
- <b>Develop on master branch of all repos</b>
- <b>Build client from latest master and connect to latest-release
  servers</b>
  We should be able to play with everyone on a client with the latest
  bug fixes.
- <b>Build server from latest master and host with latest-release
  DPKs</b>
  Likewise with a server.
- <b>Develop Unvanquished on master, using latest-release DPKs</b>
  Development for simple cases should be accessible, not requiring
  `-pakpath` flags etc. Compatibility with the latest-release
  `unvanquished` DPK doesn't need to be perfect; it's OK if there are a
  few warnings or slightly messed up things in the UI. But it should be
  usable for basic experimentation.

### Use cases we don't really care about

- <i>Using cgame and sgame built from different commits.</i>

## Per-repository guidance

### Daemon

Adding or removing an IPC call must be done on the next-release branch.

When developing Daemon master, you need to keep in mind compatibility
with both the latest release and the current master of the gamelogic.

### Unvanquished

Try to keep the submodule pointer to Daemon at a commits which is
compatible with the Unvanquished commit containing them. We want to get
a harmonious set of components when we do a recursive checkout of some
Unvanquished commit.

Changing the `playerState_t` netcode is acceptable because the netcode
table is stored in the gamelogic and we recommend always building cgame
and sgame together.

It's OK to put gameplay changes on master. As of May 2022, we have a
nightly build server, so it would be nice to be able to test them there.

### \*.dkpdir repos from UnvanquishedAssets

There isn't a lot of precedent here. Probably it's best to do anything
except bug fixes on a next-release branch. If possible, we want to avoid
any situation where developers are required to use any unreleased stuff
from these to get a working setup.