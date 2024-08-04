---
title: Tools DaemonMediaAuthoringKit
permalink: /Tools/DaemonMediaAuthoringKit/
---

The [Dæmon Media Authoring
Kit](https://github.com/DaemonEngine/DaemonMediaAuthoringKit) is a CMake
recipe to build common tools to build assets.

It can build and install:

- (game level editor) with NetRadiant Unvanquished gamepack;

- (game level compiler);

- (navmesh generator);

- (level rextexturing tool);

- (material generator);

- (asset builder and packager);

- (CRN texture compressor);

- (model compiler);

- cwebp (WebP image converter);

- flac (FLAC audio converter);

- opusenc (Opus audio converter);

- oggenc (Vorbis audio converter).

See [Tools](Tools "wikilink") for details about Unvanquished tools.

## How to build and install

    git clone https://github.com/DaemonEngine/DaemonMediaAuthoringKit.git
    cmake -H. -Bbuild
    cmake --build build -- -j$(nproc)

CMake will download sources, compile them and install binaries and other
files in the `install` folder.

## How to use

You can then add the `install/bin/` directory to your `PATH` environment
variable:

    export PATH="${PATH}:$(pwd)/install/bin"

After that, you can call every tool from command line, for example
`netradiant`, `chameleon`, `urcheon`, etc.

[Category:Tools](Category:Tools "wikilink")