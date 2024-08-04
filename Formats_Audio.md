---
title: Formats Audio
permalink: /Formats/Audio/
---

The terms <dfn>lossy</dfn> and <dfn>lossless</dfn> are used multiple
times in this page. Lossy means that sound files compressed using that
format will lose some of their audio fidelity to save space. Lossless
means that the compression will not sacrifice audio fidelity, no matter
how much you compress the sound file with that format.

## Tools

See [Tools/Audio](Tools_Audio "wikilink").

## Licensing

The following licenses are suitable for music and sounds:

## Supported formats

- Opus — a lossy compressed format, ;
- Vorbis — a lossy compressed format, ;
- Wav — a lossless uncompressed format, , .

The expects the Vorbis files to use the file extension and the Opus
files to use the file extension.

## Recommended audio formats

### Recommended formats in repositories

It's recommended to store data files in well-known compressed lossless
formats in data repositories.

There is no lossless compressed audio format supported by the engine.

Convert Wav files and other lossless audio files to FLAC to store them
in repositories. The choice of FLAC in repositories is a convention, and
the package builder knows how to convert from FLAC to Opus.

It's better to compress to specific formats (Opus) while you distribute
your work for use in game, but please keep them lossless and in
widely-used formats in repositories!

If your original file is already in OGG Vorbis or Opus lossy format,
store it in repository as is without recompressing it to another format
to avoid losing more data.

## Configuration files

### Buildables

There are 14 animations per buildable type: *construct1*, *construct2*,
*idle1*, *idle2*, *idle3*, *attack1*, *attack2*, *spawn1*, *spawn2*,
*pain1*, *pain2*, *destroy1*, *destroy2*, and *destroyed*. Each
buildable type has a sound configuration file, located at
*sound/buildables/<var><buildable_type></var>/sound.cfg*, that describes
2 properties for each buildable animation:

- whether the buildable animation has an associated sound, and
- whether the sound is to be played in a loop.

Such a file should contain a <em>1</em> for a <em>yes</em> answer and a
<em>0</em> for a <em>no</em> answer, for the above 2 questions, in the
given order, and for each buildable animation, in the above given order.
Technically, this means that the file should contain 28 integers (2 per
animation). However, by convention, 1 line is used for each animation,
and comments are added for guidance about which animation a pair of
numbers refers to.

So each line in a buildable sound configuration file is formatted as
follows:

<var><has_sound></var>` `<var><loop></var>` //`<var><filename></var>

This is an sound configuration file example for a buildable:

    1 0 //construct1.wav
    0 0 //construct2.wav
    1 1 //idle1.wav
    0 0 //idle2.wav
    0 0 //idle3.wav
    0 0 //attack1.wav
    0 0 //attack2.wav
    0 0 //spawn1.wav
    0 0 //spawn2.wav
    0 0 //pain1.wav
    0 0 //pain2.wav
    1 0 //destroy1.wav
    1 0 //destroy2.wav
    0 0 //destroyed.wav

Do not reorder the lines because it's how the game knows what is what.
The comments are for humans only!

## Sound filenames

The structure `cg_customSoundNames` in
[src/gamelogic/gpp/src/cgame/cg_players.c](https://github.com/TremZ/Unvanquished/blob/master/src/gamelogic/gpp/src/cgame/cg_players.c)
contains a list of some sounds.

[Category:Formats](Category:Formats "wikilink")
[Category:Audio](Category:Audio "wikilink")