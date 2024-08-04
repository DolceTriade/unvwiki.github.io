---
title: Formats RoQ
permalink: /Formats/RoQ/
---

The RoQ video format is a legacy format inherited from legacy id Tech
engines.

## Usage

The only usage of RoQ videos in the is to be used on in-game surfaces
using the material keyword.

In practice any resolution is supported, as long as the dimensions are
divisible by 16. The sound channel will be ignored.

Here is a command to convert a given into a :

`ffmpeg -i video.webm -an -vf scale="256:256" -r 30 video.roq`

## History

The [Multimedia Wiki](https://wiki.multimedia.cx/index.php?title=RoQ)
says:

> RoQ is a full motion video format originally developed for The 11th
> Hour by Graeme Devine. The format was later used as the FMV format for
> Quake III: Arena and derivative games.
>
> According to excerpts of Devine's 11th Hour development journal
> published in Wired at
> <http://www.wired.com/wired/archive/3.08/shipping.html>, the RoQ
> format was named after Devine's newborn daughter, Roqee.

The [Edge wiki](https://3dfxdev.net/edgewiki/index.php?title=ROQ_Videos)
also says:

> RoQ is a video file format that originated in The 11th Hour game.
> After Graeme Devine, the creator of the format joined id Software, the
> RoQ file format has been in use in every game the company has released
> such as Quake III, Return to Castle Wolfenstein and DOOM 3.

## Format

The format only supports 30 frames per second framerate. There is a
space designated for FPS in the file header, but it is ignored by the
reference implementation.

About video resolution in predecessor engines, the Edge wiki says:

> Videos may technically be up to 65520 x 65520 pixels with both
> dimensions divisible by 16 and produce a valid RoQ file, but none of
> id Software’s games will play back a video with dimensions that aren’t
> a power of two, most likely because of OpenGL’s texture sizing
> restrictions.

The [OpenArena wiki](https://openarena.fandom.com/wiki/RoQ) says that
Quake Ⅲ was able to use video resolutions up to for cinematic and that
video resolution should not be greater than to be played as an in-game
surface with the material keyword. The doesn't support cinematic but
supports the material keyword.

The RoQ format supports mono, stereo, with 22050 Hz being the only rate
supported, or the absence of any audio channel. We have no usage for RoQ
sound in the .

The ffmpeg video codec is and the audio codec is .

[Category:Formats](Category:Formats "wikilink")
[Category:Video](Category:Video "wikilink")