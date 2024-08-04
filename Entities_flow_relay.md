---
title: Entities flow relay
permalink: /Entities/flow_relay/
---

## target_relay (0 .7 .7) (-8 -8 -8) (8 8 8) HUMAN_ONLY ALIEN_ONLY RANDOM

This can only be activated by other triggers which will cause it in turn
to activate its own targets. If wait, delay or the random time variance
is set, it will wait until it is relaying by firing its targets, much
like the former target_delay

targetname, targetname2, targetname3, targetname3: activating trigger points to one of these.
target, target2, target3, target4: this points to entities to activate when this entity is triggered. RANDOM chooses whether all gets executed or one gets selected Randomly.
wait: delay in seconds from when this gets triggered to when it fires its own targets (default approx. 1).
waitVariance: random time variance in seconds added or subtracted from "wait" delay (default 0 - see Notes).

### SPAWNFLAGS

HUMAN_ONLY: only human team players can activate trigger.
ALIEN_ONLY: only alien team players can activate trigger.
random: one one of the targeted entities will be triggered at random.

### NOTES

When the random key (not to be confused with the RANDOM-spawnflag) is
set, its value is used to calculate a minimum and a maximum delay. The
final time delay will be a random value anywhere between the minimum and
maximum values: (min delay = wait - random) (max delay = wait + random).