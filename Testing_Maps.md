---
title: Testing Maps
permalink: /Testing/Maps/
---

## Cheat commands and cvars

- To fly around the map, use the `\noclip` command.
  If you find that you are moving too slowly (or too fast), you may
  change the speed with `cg_flySpeed`.
- To make yourself invincible, use the `\god` command.
- To stop buildables from attacking, use the `\notarget` command.
- To publicly test your maps, make a thread [on
  forums](https://forums.unvanquished.net/viewforum.php?f=9) to share
  your work-in-progress work and some server admins will probably host
  it ;-).
- To lock the state of PVS, set `r_lockpvs` to `1`. Be aware of the
  difference between this and `r_novis`: this disables any *updates* to
  the state of the PVS buffer but PVS is still in effect; this can make
  flying outside of a map difficult.
- To disable PVS entirely, set `r_novis` to `1`.
- To disable PVS for entities, set `sv_novis` to `1`.

[Category:Testing](Category:Testing "wikilink")
[Category:Mapping](Category:Mapping "wikilink")