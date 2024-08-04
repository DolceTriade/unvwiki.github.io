---
title: Tools Crunch
permalink: /Tools/Crunch/
---

Crunch is a texture compressor producing formats optimized for both GPU
processing and distribution.

Unvanquished recommends the Dæmon crunch which is maintained by
ourselves and is based on the Unity version.

The crunch tool was initially written by BinomialLLC then improved by
Unity. Neither BinomialLLC neither Unity have merged our fixes and does
not seem to have any interest in merging fixes provided by others, so we
started to also merge fixes from others.

## Sources

The Crunch source repository is:
[github.com/DaemonEngine/crunch](https://github.com/DaemonEngine/crunch).

The repository provides the **crunch** tool, the **crnlib** library to
provide full compression/decompression support to third-party
applications, and the header-only library which is enough to transcode
the CRN data for GPU upload and is perfect for lightweight integration
in renderers. Some examples implementing various kinds of integrations
are provided.

## Portability

We take care of cross-platform compatibility and we make sure the tool
is buildable with CMake.

The Dæmon crunch repository is known to build with various compilers,
and the Dæmon crunch tool is known to run on Linux, Windows, macOS and
FreeBSD systems on various hardware architectures.

## Quality

A continuous integration pipeline is configured to test the building of
the tool and the library themselves and to run some tests. The code is
frequently submitted to CodeQL static analysis.

## Formats

Crunch can produce compressed images optimized for games in various
formats like DDS, KTX and CRN.

All those three formats are containers for DXT-compressed bitmaps. This
DXT-compressed data can be uploaded directly to the GPU memory without
decompression, and the GPU can process DXT-compressed data without
decompression.

Crunch writes DXT-compressed data in a way an additional compression
performs better on them, especially LZMA. For example, produced DDS
images are expected to compress well if repackaged in an LZMA-based
archive.

The CRN format does all of this in one go: it stores the DXT-compressed
data into a custom LZMA container.

The game engine or any other application processing CRN files just have
to unpack the LZMA container using provided functions and to upload the
DXT-compressed data to the GPU.

The Dæmon crunch sets the header field to to make it compatible with
Unity.

## Performance

The Dæmon crunch runs multiple time faster than the original crunch,
thanks to the work done by Unity. Unity people claimed the tool runs 2.5
time faster, and we measured the tool running 4.3 time faster on the
Unvanquished corpus. Unity people claimed the tool compresses about 10%
better, we measured more than 11% on the Unvanquished corpus. This
performance bump comes with a compatibility-breaking change introduced
in the Unity branch.

The files produced by the Dæmon crunch are then readable by both the
Unity crunch and the Dæmon crunch but not by the original Binomial
crunch, while the files produced by the original Binomial crunch are not
readable by the Unity crunch and the Dæmon crunch. The Binomial crunch
isn't maintained anymore.

## Features

The Dæmon crunch provides many improvements over the original crunch:

- ✅️ Unity crunch format (runs many time faster and produces smaller
  files),
- ✅️ Unity crunch metadata (the header is compatible with Unity),
- ✅️ Improved image compatibility (1-bit PNG images are now supported),
- ✅️ Added features and command line options (top mip renormalization
  and more),
- ✅️ Network file system compatibility,
- ✅️ Optional header-only checksumming,
- ✅️ Multisystem and multiplatform (runs almost everywhere),
- ✅️ CMake toolchain (with many useful build options).

More details and up-to-date information can be found in the [project
README](https://github.com/DaemonEngine/crunch/blob/master/README.md).

## Support

The Dæmon crunch is known to be used by the project itself, the , the
Xonotic game (as DDS converter) and some other games using the Unity
game engine. It is also used in production tools like
[Urcheon](Tools_Urcheon "wikilink"),
[NetRadiant](Tools_NetRadiant "wikilink"), and
[Q3map2](Tools_Q3map2 "wikilink").

## How to use Crunch

[Category:Tools](Category:Tools "wikilink")