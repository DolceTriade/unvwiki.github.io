---
title: Formats Known regressions since Tremulous
permalink: /Formats/Known_regressions_since_Tremulous/
---

As a mapper or someone creating assets for the game, you may be aware of
those pitfalls that can be considered as regressions when comparing with
Tremulous or Quake Ⅲ.

See also the [Limitations that are not
regressions](Formats_Limitations_that_are_not_regressions "wikilink")
page for things that are not regressions.

## Regressions that may make the game look broken

### Missing portal blending

Portal blending is not implemented yet in the renderer.

What happens is that the renderer that was used in Quake Ⅲ and Tremulous
were OpenGL 1 renderers, and the Dæmon engine renderer is an OpenGL 3+
renderer. The difference between OpenGL 1 and OpenGL 3+ is similar to
the difference between OpenGL 4.6 and Vulkan. Those renderers are
different software. Everything from the OpenGL 1 renderer had to be
re-implemented in OpenGL 3+ renderer with new code.

So the lack of portable blending is not technically a regression as the
code never existed in the renderer to begin with. It also means there is
no bug in our code.

Though, we fully agree this means a map ported from Tremulous that was
using that feature will look broken and that then can be considered as a
regression from a player or mapper point of view.

From the code point of view, this is a feature request and we need
someone to implement it. We are looking for renderer developers and
OpenGL 3+ specialist to implement the feature in our engine.

### "Autosprite" shaders don't work

See [Daemon#322](https://github.com/DaemonEngine/Daemon/issues/322).

## Regressions that may make the game look broken, but with workaround

### Stereo sound effect not being positional

Currently only mono sound files are played properly as positional audio,
stereo sound files are played *in your face*. We need to fix this.

A simple workaround can be applied when repackaging the files: just
convert the positional stereo sound as mono, this would make no
difference to the player (stereo positional sound is meaningless
anyway).

## Regressions that don't make the game look broken

### Missing alphaGen lightingSpecular

The was a subtle effect applied on some textures. This feature being
missing doesn't break the rendering of the texture and if you look at
the surface you may not notice something is wrong, unless you do
comparative screenshots with Tremulous and Unvanquished. [Github
issue](https://github.com/DaemonEngine/Daemon/issues/213)

Implementing this feature has very low priority as there is no impact on
gameplay and textures don't look bad without it. The game doesn't look
broken without it and one cannot know the feature is missing just by
playing the game, unless some warning tells it in log.

[Category:Formats](Category:Formats "wikilink")