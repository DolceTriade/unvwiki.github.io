---
title: Entities path corner
permalink: /Entities/path_corner/
---

## path_corner (.5 .3 0) (-8 -8 -8) (8 8 8)

Path corner entity that func_trains can be made to follow.

target, target2, target3, target4: point to next path_corner in the path and/or other targets to fire when the path corner is reached
targetname, targetname2, targetname3, targetname3: the train following the path or the previous path_corner in the path has to point to one of these.
speed: speed of func_train while moving to the next path corner. This will override the speed value of the train.
wait: number of seconds func_train will pause on path corner before moving to next path corner (default 0 - see Notes).

### NOTES

Setting the wait key to -1 will not make the train stop on the path
corner, it will simply default to 0.