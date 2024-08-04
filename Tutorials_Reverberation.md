---
title: Tutorials Reverberation
permalink: /Tutorials/Reverberation/
---

## What it is

Reverberation is the effect of a sound lasting after it has been
produced because of its the mutiples echos in the environment. It can
give great audio clues as to what environment you are in: you would
easily distinguish sounds in a regular room from sounds in a hangar from
sounds in outdoor based on the reverberation.
[Wikipedia](http://en.wikipedia.org/wiki/Reverberation) has some
examples of reverberation.

Dæmon supports reverberation effects, which you can try using the
*/testReverb* command (use tab completion to see the list of presets),
it can be used in maps to give audio clues of the size of rooms and the
material of their walls. However even if reverberation effects sound
really cool, you should be subtle when using it: in real life you barely
notice these effects unless you are in churches or hangars.

## Mapping reverberation

### Global reverberation

Once you have found a reverberation effect you like with */testReverb*
you can apply it on the whole map by setting the following keys on the
worldspawn.

- **reverbEffect <presetname>**: with <presetname> the name of the
  effect to apply globally
- **reverbIntensity <number>**: with <number> between 0 and 2 the
  intensity of the effect. The default is 1.0 so you can lower the
  effect or

crank it up to your liking (but it should mainly be used to lower the
effect).

### Localised reverberation

You can also define reverberation effects per area by placing
func_static entities and adding the following keys to it:

- **reverbEffect <presetname>**: like for the worldspawn
- **reverbIntensity <number>**: like for the worldspawn
- **reverbDistance <distance>**: a distance in qunits representing the
  approximate size of the room in which to use the effect. Between such
  func_statics, effects will be blended, potentially with the global
  reverb effect.

[Category:Tutorials](Category:Tutorials "wikilink")
[Category:Mapping](Category:Mapping "wikilink")