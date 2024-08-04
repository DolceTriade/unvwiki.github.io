---
title: Bug reporting
permalink: /Bug_reporting/
---

Please file any bugs you find on GitHub issue tracker.

Before filing a bug report, please check the
[Troubleshooting](Troubleshooting "wikilink") page, browse the [support
forums](https://forums.unvanquished.net/viewforum.php?f=6), and search
the [default issue
tracker](https://github.com/Unvanquished/Unvanquished/issues) to see if
your issue has been noticed or reported before.

Some of the tips on the [Testing](Testing "wikilink") page may be useful
to produce good reports.

## Issue trackers

There are separate issue trackers for separate parts of the game and the
project:

- **Game** (ℹ️ In doubt, use this one):
  [github.com/Unvanquished/Unvanquished/issues](https://github.com/Unvanquished/Unvanquished/issues)
- **Game data** (map, texture, models, sound file…):
  [github.com/UnvanquishedAssets/UnvanquishedAssets/issues](https://github.com/UnvanquishedAssets/UnvanquishedAssets/issues)
- **Engine** (rendering bugs…):
  [github.com/DaemonEngine/Daemon/issues](https://github.com/DaemonEngine/Daemon/issues)
- **Updater/launcher**:
  [github.com/Unvanquished/updater/issues](https://github.com/Unvanquished/updater/issues)
- **Master server**:
  [github.com/Unvanquished/unvanquished-master/issues](https://github.com/Unvanquished/unvanquished-master/issues)
- **Website**:
  [github.com/Unvanquished/unvanquished-infrastructure/issues](https://github.com/Unvanquished/unvanquished-infrastructure/issues)

## Reporting issues

Please try to do the following when writing a bug report:

- Describe the problem in detail. Carefully note what actually happens
  and what you expected to happen.
- Describe how to reproduce the problem: i.e., steps that the developers
  can follow to cause it to happen.
- Do not post console logs or error messages without any other
  accompanying explanation with the expectation that the developers will
  solve your problem for you; you must provide details!
- If the problem is best explained with a picture or video, please, take
  a [screenshot](Taking_screenshots "wikilink") and/or [record a
  demo](Recording_demos "wikilink")!

Please include hardware / software specs when you report your bug. Use
the following template:

    ### Hardware / Software

    | Release |
    |:--|:--
    | Operating System |
    | Video Card |
    | Driver Type |
    | Driver Version |
    | OpenGL Version |
    | Map tested |

If you are on Linux, please also include fields for your kernel version
(which you can obtain from `uname`) and driver type (i.e., proprietary
or open source).

For example, your information might look like this:

    ### Hardware / Software

    | Release | v0.13.0
    |:--|:--
    | Operating System | Ubuntu 12.04 LTS
    | Kernel Version | 3.2.0-38-generic
    | Video Card | ATI Radeon HD 5670
    | Driver Type | Proprietary (fglrx)
    | Driver Version | 8.85-110419a118915C-ATI (Catalyst 11.5)
    | OpenGL Version | 4.2.11903 Compatibility Profile
    | Map tested | Star A.T.C.S.

which will produce a table like so:

| Release          | v0.13.0                                 |
|------------------|-----------------------------------------|
| Operating System | Ubuntu 12.04 LTS                        |
| Kernel Version   | 3.2.0-38-generic                        |
| Video Card       | ATI Radeon HD 5670                      |
| Driver Type      | Proprietary (fglrx)                     |
| Driver Version   | 8.85-110419a118915C-ATI (Catalyst 11.5) |
| OpenGL Version   | 4.2.11903 Compatibility Profile         |
| Map tested       | Star A.T.C.S.                           |
|                  |                                         |

## Do's and Don'ts

- **Do** include the requested information listed above.
- **Do** describe the issue with the bug title. A title of just
  "Console", for example, does nothing to describe the issue at hand
  and, as such, makes the issue more difficult to return to for
  developers, as well as for developers to gauge the impact of the
  issue. Issues with titles such as "Opening the menu **causes the game
  to crash**" will be more likely to be read by a developer than the
  same issue titled "Menu bug", for example.
- **Do not** refer to forum posts or similar anecdotally without
  providing a link.
- **Do not** include extraneous information.
- **Do** check to ensure that your grammar and spelling is correct.
- **Do** use Markdown headers (begin a line with some number of pound
  signs, e.g., `###`) to delineate sections of your report.

## Formatting Tips & Tricks

### Code Blocks

To delineate a block of code (and enable special formatting such as
syntax highlighting), begin and end the code block with three backticks
(\`):

```` ``` ````
`/* code */`
```` ``` ````

This makes reports with console output much easier to read and makes it
unnecessary to rely on outside paste services.

To enable syntax highlighting, you must specify a language following the
first set of backticks:

```` ```c++ ````
`/* code */`
```` ``` ````

The following language keywords are known to work:

- `diff`
- `javascript`
- `c`
- `c++`
- `python`