---
title: Map Layouts
permalink: /Map_Layouts/
---

Note: this page is just a dumping of useful informations to create an
alternative layout which can be used either by vote or by rotation. Note
that the server must have access to the layout for this to work.

- `/devmap MAPNAME`: required to use most of the commands
- `/g_instantBuilding`: makes building instant, and removes the
  cooldowns before next building
- `/noclip`: allows the user to travel through walls and ignore gravity
- `/devteam [a|h]`: spawn where you are as either naked human with CKit
  or adv granger
- `/give momentum`: give your team maximum momentum, so that you're not
  limited by momentum for now (it will still decrease with time).
  Specific number can be provided. Negative number removes stuff.
- `/give bp`: give your team a lot of BP. Specific number can be
  provided. Negative number removes stuff.
- `/layoutSave LAYOUTNAME`: saves the layout with the name LAYOUTNAME
- `/layoutLoad LAYOUTNAME`: loads the layout with the name LAYOUTNAME
- `/cg_drawBBox 1`: allows one to see the collisions of the buildings

If you want test bots with alternative IA, like one on SK servers, you
must follow these steps:

- If you never already loaded a map on SK server, you must load any map
  on any SK server first. This will download extrapack files.
- /set fs_extrapaks mod-betterai
- /bot fill 5 a 9 will load 5 alien bots with level 9 (level is 1 to 9)
- /bot fill 5 h 9 will load 5 human bots with level 9 (level is 1 to 9)