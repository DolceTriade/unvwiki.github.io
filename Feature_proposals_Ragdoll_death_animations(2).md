---
title: Feature proposals Ragdoll death animations
permalink: /Feature_proposals/Ragdoll_death_animations/
---

Currently, death animations must be created by hand by an animator,
which is a time consuming process. As such, the number of death
animations is finite and typically very little. A death animation that
would otherwise stand on its own might look terrible in certain gameplay
contexts, as well; for example, an animation of a human falling to the
floor that they are standing on looks awful when played as said
character is falling through space.

## Specific behaviors

### Trapper

The trapper (and likely other alien structures, in future) poses an
interesting problem in that it remains attached to the ceiling when it
dies, but one would expect its tail to fall down and flop about
realistically. As it stands now, the death animation only looks correct
when it is built on the floor. A simple Newtonian particle physics
system with springs should do to procedurally calculate positions of the
tail bones.

[Category:Feature proposals](Category:Feature_proposals "wikilink")