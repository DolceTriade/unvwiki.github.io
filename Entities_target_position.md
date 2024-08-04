---
title: Entities target position
permalink: /Entities/target_position/
---

## target_position (0 .5 0) (-8 -8 -8) (8 8 8)

Used as a positional target for in-game calculation. Other entities like
light, misc_portal_camera and trigger_push (jump pads) might use it for
aiming.

targetname, targetname2, targetname3, targetname3: the names under which this position can be referenced

also if used as teleport destination:

angle: direction in which player will look when teleported to this position

### NOTES

To make a jump pad, place this entity at the highest point of the jump
and target it with a trigger_push entity.