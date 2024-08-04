---
title: GSoC idea list
permalink: /GSoC_idea_list/
---

# Note to students

This is a curated list of ideas suggested by regular developers. They
vary in difficulty but are all doable during the summer. Of course feel
free to add your own ideas to the list, respecting the current format
(leave Mentor empty). You can also drop by the IRC channel to discuss
your ideas, also note that you can get involved in gameplay too!

# Engine

## Sound shaders

- **Brief explanation:** Our engine supports only sounds, with no
  information attached and the little sound effects we have need to be
  handled in a case by case by the gamelogic. Sound shaders would be
  sets of parameters associated to a sound file that would allow things
  like: randomizing samples, changing the attenuation model, looping,
  sound category, ...
- **Expected results:** Sound shaders are implemented and used in a few
  maps to enrich the audio environment.
- **Prerequisite knowledge:** C++.
- **Mentor:** Corentin "kangz" Wallez

## Use bullet for physics

- **Brief explanation:** The Quake3 physics code we use is very limited
  in both that it only handles collision with the world and supports
  mostly axis-aligned boxes. Using bullet would overcome this
  limitations and open the way for more advaned features such as inverse
  kinematics, ragdolls and more accurate physics simulation.
- **Expected results:** All the physics call go through bullet instead
  of the former physics system, while keeping mostly the same physics.
- **Prerequisite knowledge:** C++, vector math, game physics library a
  big plus.
- **Mentor:** Corentin "kangz" Wallez

## Breakpad integration

- **Brief explanation:** We want to make it easy for users to submit
  useful crash reports. Google Breakpad is a good solution. In the
  future, we can even discuss an option to automatically send these to
  us (with the user's permission) and create an issue on github.
- **Expected results:** At least on Windows, a crash of the engine
  produces a dump that contains useful debug info. Better, the crash
  handler asks the user if they want to upload it to our servers.
- **Prerequisite knowledge:** C++, will require access to a windows
  machine for testing.
- **Mentor:** Corentin "kangz" Wallez (Amanieu d'Antras)

## Renderer support for GL ES 3

- **Brief explanation:** Our renderer relies on GL 2.1 + extension or GL
  3, the goal is to add support for GL ES 3, potentially removing GL 2.1
  support. This would allow us to port the on platforms without Desktop
  OpenGL support such as the Web and mobile platforms.
- **Expected results:** The game engine can run without linking to
  libGL, or better is shown running on the web / mobile.
- **Prerequisite knowledge:** C++, OpenGL.
- **Mentor:** Corentin "kangz" Wallez

## Add debug draw capabilities

- **Brief explanation:** Printf debugging is nice but sometimes it is
  easier to visualize things than to read them, especially for 3D. We
  want to add draw debugging to help debugging the gamelogic or
  subsystems that work with 3D objects, the goal is to have a super
  simple interface to draw basic geometry, in all parts of the engine
  and gamelogic.
- **Expected results:** Basic shapes (spheres, boxes, arrows) and text
  can be drawn in the 3d world with control for color, depth test and
  wireframe mode.
- **Prerequisite knowledge:** C++, vector math, OpenGL a plus.
- **Mentor:** Corentin "kangz" Wallez

## Input thread / Splashscreen

- **Brief explanation:** It'd be nice to have a splash screen while the
  game starts (6 sec on my SSD with hot OS cache). Also we will want
  inputs to be processed in parallel of the game to reduce latency and
  enable neat tricks. The two are linked since with SDL all the
  windowing function must be done in the main thread, including getting
  new events.
- **Expected results:** The splashscreen and input thread are
  implemented.
- **Prerequisite knowledge:** C++, some multithreading.
- **Mentor:** Corentin "kangz" Wallez

# Updater

## Add news support

- **Brief Explanation:** Every player will see the updater and this
  gives us an oppurtunity to engage players that wouldn't otherwise be
  part of the "community". The goal is to fetch news from the site and
  display it in a pleasing manner
- **Expected Results:** Implement both the frontend of this in the
  updater and a simple backend where news are published.
- **Prerequisite knowledge:** QT, C++
- **Mentor:** Harsh "\`Ishq" Modi

## In game integration

- **Brief Explanation:**We need to be able to launch the updater frmo
  the game when an update is found, in a cross platform way otherwise we
  would be keeping the update manual as it is currently which defeats
  the purpose of the updater.
- **Expected Results:** Message should show up ingame telling player to
  update. Clicking on message should launch updater to update the game.
- **Prerequisite knowledge:** C++
- **Mentor:** Harsh "\`Ishq" Modi