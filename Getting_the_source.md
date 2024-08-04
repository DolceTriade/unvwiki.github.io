---
title: Getting the source
permalink: /Getting_the_source/
---

## Installing Git

See [Installing Git](Tools_Git#Installing_Git "wikilink").

## Downloading the source

### Command line

The following commands will work on any platform.

    git clone --recurse-submodules https://github.com/Unvanquished/Unvanquished.git

This will create a directory called *Unvanquished*.

If you already cloned but forgot to use the option:

`cd Unvanquished`
`git submodule update --init --recursive`

If you would like to get the source for a particular version, [check
out](http://git-scm.com/docs/git-checkout) the associated
[tag](http://git-scm.com/book/en/Git-Basics-Tagging):

`cd Unvanquished`
`git checkout `

To see the list of tags (versions) available to check out,

`git tag`

will produce a list.

### Linux

Please see the [command line](#Command_line "wikilink") instructions.

### macOS

#### Command Line

Open a Terminal (`/Applications/Utilities/Terminal`) and follow the
[command line](#Command_line "wikilink") instructions.

#### Xcode 4

1.  Start Xcode.
2.  Open the Organizer window (Window → Organizer or )
3.  Hit the "Repositories" button on the top bar.
4.  Hit the "+" button in the lower-left corner, and choose "Checkout or
    Clone Repository…".
5.  In the rollout sheet that appears, enter
    [`https://github.com/Unvanquished/Unvanquished.git`](https://github.com/Unvanquished/Unvanquished.git)
    into the "Location" field, and hit "Next".
6.  Enter "Unvanquished" into the "Name" field, ensure that the "Type"
    combo box is set to "Git", and hit "Clone".
7.  You will be prompted where to save the repository. Choose a location
    and hit "Clone".

### Windows

#### TortoiseGIT

1.  Make and enter a new folder to store the source code in
2.  Right click the inside of the folder → Git Clone...
3.  In the Url textbox enter:
    [`https://github.com/Unvanquished/Unvanquished.git`](https://github.com/Unvanquished/Unvanquished.git)
4.  Hit OK.

#### Command Line

Open the MsysGit terminal and and follow the [command
line](#Command_line "wikilink") instructions.

## Keeping your copy of the source up-to-date

For more information on using git, an excellent resource is the official
[git book](http://git-scm.com/book), available to read online for free.

### TortoiseGit

1.  Right-click somewhere in the source directory, and choose "Git
    Sync".

### Command-line (All platforms)

To pull (i.e., fetch and merge) changes made since you checked out the
source—that is, to update your working copy to match the current state
of the official repository—you (typically) need only run one command:

`$ git pull origin master`

## Compiling

After getting the source code, you can
[compile](Compiling_the_source "wikilink") it.