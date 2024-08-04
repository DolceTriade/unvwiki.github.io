---
title: Entities sensor timer
permalink: /Entities/sensor_timer/
---

## trigger_timer (0 .5 .8) (-8 -8 -8) (8 8 8) START_ON

Time delay trigger that will continuously fire its targets after a
preset time delay. The time delay can also be randomized. When
triggered, the timer will toggle on/off. Formerly known as func_timer.

wait: delay in seconds between each triggering of its targets (default 1).
waitVariance: random time variance in seconds added or subtracted from "wait" delay (default 0 - see Notes).
target, target2, target3, target4: this points to the entities to trigger.
targetname, targetname2, targetname3, targetname3: any triggering entity that targets one of these names will toggle the timer on/off when activated.

### SPAWNFLAGS

START_ON: timer will start on in the game and continuously fire its targets.

### NOTES

When the random key is set, its value is used to calculate a minimum and
a maximum delay. The final time delay will be a random value anywhere
between the minimum and maximum values: (min delay = wait - random) (max
delay = wait + random).