---
title: Tools Iqmtool
permalink: /Tools/Iqmtool/
---

==Sources==

The iqmtool source repository is:
<https://sourceforge.net/p/fteqw/code/HEAD/tree/trunk/iqm/>

## Features

Like upstream `iqm` tool, `iqmtool` can compile `.iqe`, `.md5mesh` and
`.md5anim` files to `.iqm` files and can can embed model (multiple
meshes) and animations in a single file.

This tool also supports translation, rotation and scaling operations on
models with operations applied on animations too.

## Getting the tool

Initially named `iqm`, the latest versions of this tool are now named
`iqmtool` to be able to have both original `iqm` and modified FTEQW
`iqmtool` binaries in `PATH`.

### Simple build

You don't have to fetch the whole fteqw repository to build iqmtool, you
can just fetch the iqm subdirectory and use the Makefile present there
to build iqmtool. This is the lightest and fastest way to build iqmtool,
and the tool will have enough features for contributing to Unvanquished:

    svn checkout https://svn.code.sf.net/p/fteqw/code/trunk/iqm iqmtool
    cd iqmtool
    make

You'll find `iqmtool` there.

### Complete build

It's also possible to build iqmtool with support from other formats,
like importing from glTF, for that you need to build it against fteqw
plugins, so that means you need to fetch the whole fteqw repository
instead:

    svn checkout https://svn.code.sf.net/p/fteqw/code/trunk fteqw
    cd fteqw
    make -C engine iqmtool

You'll find `engine/release/iqmtool`.

## Other tools

See also [Tools/IQM](Tools_IQM "wikilink").

[Category:Tools](Category:Tools "wikilink")
[Category:IQM](Category:IQM "wikilink")