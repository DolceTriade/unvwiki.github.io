---
title: UI Implementation
permalink: /UI/Implementation/
---

## Weapon icons

Weapon icons are controlled by the `icon` entry in the weapon's
[configuration file](Exporting_Models#Weapons_2 "wikilink").

## libRocket GUI

A move to use [libRocket](http://librocket.com/) has been planned with
support underway. This middleware will allow creating the user interface
using HTML and CSS. If you are interested in assisting with the
transition, please [contact a member of the
team](Main_Page#Contributing "wikilink") to find out how to help.

### libRocket Integration Progress

#### General

- Get libRocket to play nicely with q3 shaders \[woo, done\]
- Clean up the generic RocketElement class used to draw all the
  ownerdraws \[75%\]
- Remove ui_shared.c cgame dependence \[50%\]
- Analyze potential of adding future animations \[waaaaaaaaaay in the
  future, if at all\] [DukeNukem3D
  Megaton](https://github.com/TermiT/duke3d-megaton/tree/master/code/rocket)

#### Data Sources (aka feeders)

| Name              | Description                                                                  | Status                  |
|-------------------|------------------------------------------------------------------------------|-------------------------|
| Resolutions       | list of resolutions                                                          | Implemented             |
| VoIP Input        | Input devices for OpenAL                                                     | Implemented             |
| AL Output         | Output devices for OpenAL                                                    | Implemented             |
| HUDS              | List of HUDs to choose from                                                  | Not Implemented         |
| Languages         | List of languages                                                            | Implemented             |
| Mods              | List of mods                                                                 | Implemented             |
| Demos             | List of demos                                                                | Implemented             |
| Maps              | List of maps                                                                 | Implemented             |
| Players on team   | List of players on each team                                                 | Implemented             |
| Players           | List of players. This and above can probably be combined.                    | Combined with the above |
| Server status     | Detailed information on a server // Probably can implement without a feeder. | Implemented             |
| Find player       | Results for a multiserver player search.                                     | Not Implemented         |
| Team list         | List of available teams                                                      | Implemented             |
| Classes           | List of classes per team                                                     | Implemented             |
| Items             | List of available items per team                                             | Implemented             |
| Armory items      | List of items. Can probably be merged with above.                            | Implemented             |
| Alien evo classes | List of classes that can be evo'd to.                                        | Implemented             |
| Buildable menu    | List of buildables that can be built                                         | Implemented             |
| Ignore            | List of players/patterns player has ignored                                  | Not Implemented         |
| Help              | List of help topics                                                          | Not Implementing.       |

#### Missing Elements

- Chat field - Field for chat.
- Selectable datagrid - Selectable table, essentially. Warsow has this.
  Can probably port. \[done\]
- Model view - Display a model. Low priority imo. Won't do unless there
  is demand.
- Key select - Detect which key is pressed. For binds. \[done\]

[Category:UI](Category:UI "wikilink")