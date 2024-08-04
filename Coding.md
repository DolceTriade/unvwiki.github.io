---
title: Coding
permalink: /Coding/
---

## Game

- [Getting the source](Getting_the_source "wikilink")
- [Compiling the source](Compiling_the_source "wikilink")
- [Running Unvanquished from
  Git](Tutorials_Running_Unvanquished_from_Git "wikilink")
- [Development environments](Development_environments "wikilink")
- [Making and modding](Making_and_modding "wikilink")
- [External resources](External_resources "wikilink")

## Repositories

See [Source repositories](Source_repositories "wikilink")

## New Documentation

- [Compatibility](Compatibility "wikilink") (on ensuring
  interoperability between the various software components)
- [Creating Cvars](Coding_Cvars "wikilink")

## Documentation (Possibly outdated)

- [Technical Documentation](Technical_Documentation "wikilink") has
  overviews, links and tips for getting started with the source
- [Engine](Engine "wikilink")
- [UI Implementation](UI_Implementation "wikilink")
- [GSoC idea list](GSoC_idea_list "wikilink")
- [List future ideas etherpad](List_future_ideas_etherpad "wikilink")
- [Lua in the UI](Lua_in_the_UI "wikilink")

## Contributing

- [Coding convention](Coding_convention "wikilink")
  - [Coding with intrinsics](Coding_with_intrinsics "wikilink")
  - [Reformatting the source](Reformatting_the_source "wikilink")
- [Contributing code](Contributing_Code "wikilink")

## Launch several clients for debug purpose

To launch several clients, for debug purpose or cheating, or.. more fun
(and more CPU usage...), you can use this way:

1.  create a folder somewhere,
2.  Create and go to the directory : **mkdir -p toto ; cd toto** (here
    we named it *toto* but you can choose another name),
3.  launch the client via daemon, like in Linux :
    **~/.local/share/unvanquished/base/daemon -homepath .**
4.  change configuration and player name.

If you plan to duplicate the folder, remove the publickey *pubkey* in
the folder.

To disallow mouse capture, use the command in console **/set in_mouse
0**

To move the windows on common Linux desktop, you may use *win_key* and
*left_click*.