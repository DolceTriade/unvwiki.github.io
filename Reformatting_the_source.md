---
title: Reformatting the source
permalink: /Reformatting_the_source/
---

The Daemon and Unvanquished repositories suffer from differing code
style conventions and fractally varying choice of indentation (spaces
vs. tabs). The inconsistency is a constant source of friction for
developers. I (slipher) propose that we may reformat the source code (in
one big commit) if we have all of the following:

1.  Whitespace-ignoring replacements for 'git diff' and 'git blame'
2.  A configuration file for some cross-platform formatting tool which
    produces satisfying results
3.  Instructions on how to install the formatting tool
4.  A script to rewrite a chain of commits using the formatting tool
    (for use with unmerged branches)

## Solutions

1.  freem suggests a method for configuring git blame to ignore a
    particular commit:
    - <https://www.moxio.com/blog/43/ignoring-bulk-change-commits-with-git-blame>
    - <https://git-scm.com/docs/git-blame#Documentation/git-blame.txt---ignore-revltrevgt>
      Here is a [prototype Bash
      script](https://github.com/slipher/source-tools/blob/master/wsdiff.sh)
      for doing a whitespace-ignoring invocation of git diff, which
      works by plugging into Git as an [external diff
      tool](https://git-scm.com/docs/git#Documentation/git.txt-codeGITEXTERNALDIFFcode)
      and processing both sides of the diff with clang-format. It is
      probably a bad idea to use it without specifying specific paths,
      since in that case, if used across the reformatting commit, it
      will have to process every source file in the tree.
2.  WIP: <https://github.com/Unvanquished/Unvanquished/pull/2622>
3.  ?
4.  ?

## Areas requiring special attention

Some people have noted difficulties with autoformatters and lambda
functions.
[cg_api.cpp](https://github.com/Unvanquished/Unvanquished/blob/master/src/cgame/cg_api.cpp)
is one file with a lot of lambdas.

We should consider if we want to preserve formatting of tables such as
`fields` (for map entities) in
[sg_spawn.cpp](https://github.com/Unvanquished/Unvanquished/blob/master/src/sgame/sg_spawn.cpp).