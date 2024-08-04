---
title: Entities env speaker
permalink: /Entities/env_speaker/
---

## target_speaker (0 .7 .7) (-8 -8 -8) (8 8 8) LOOPED_ON LOOPED_OFF GLOBAL ACTIVATOR

Sound generating entity that plays .wav files. Normal non-looping sounds
play each time the target_speaker is triggered. Looping sounds can be
set to play by themselves (no activating trigger) or be toggled on/off
by a trigger.

noise: path/name of .wav file to play (eg. sound/world/growl1.wav - see Notes).
wait: delay in seconds between each time the sound is played ("random" key must be set - see Notes).
waitVariance: random time variance in seconds added or subtracted from "wait" delay ("wait" key must be set - see Notes).
targetname, targetname2, targetname3, targetname3: the activating button or trigger points to one of these.

### SPAWNFLAGS

LOOPED_ON: sound will loop and initially start on in level (will toggle on/off when triggered).
LOOPED_OFF: sound will loop and initially start off in level (will toggle on/off when triggered).
GLOBAL: sound will play full volume throughout the level.
ACTIVATOR: sound will play only for the player that activated the target.

### NOTES

The path portion value of the "noise" key can be replaced by the
implicit folder character "\*" for triggered sounds that belong to a
particular player model. For example, if you want to create a
"bottomless pit" in which the player screams and dies when he falls
into, you would place a trigger_multiple over the floor of the pit and
target a target_speaker with it. Then, you would set the "noise" key to
"\*falling1.wav". The \* character means the current player model's
sound folder. So if your current player model is Visor, \* =
sound/player/visor, if your current player model is Sarge, \* =
sound/player/sarge, etc. This cool feature provides an excellent way to
create "player-specific" triggered sounds in your levels. The
combination of the "wait" and "random" keys can be used to play
non-looping sounds without requiring an activating trigger but both keys
must be used together. The value of the "random" key is used to
calculate a minimum and a maximum delay. The final time delay will be a
random value anywhere between the minimum and maximum values: (min delay
= wait - random) (max delay = wait + random).