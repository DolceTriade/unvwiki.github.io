---
title: Mentored Coding Project
permalink: /Mentored_Coding_Project/
---

To help new coders get acquainted with our code we have some mentored
coding projects. A mentored project should be:

- interesting like a new feature or some visible change
- approchable, not requiring knowledge of arcane part of the code or
  crazy templating skills (not everybody is Amanieu)
- mentored by a more experienced developer with a precise knowledge of
  that area of the code and an idea of the design of the project

[See the list of mentored
projects!](https://github.com/Unvanquished/Unvanquished/issues?labels=D-Mentored&page=1&state=open)

# Creating mentored projects

Add the task on github with the D-mentored tag. At the bottom you can
put a block like the following:

`* Mentor: Kangz (gimhael, Fuma?)`
`* Knowledge: Renderer, OpenGL, C++ hacks to make the API fluid`
`* Difficulty: 5 (without visualization) 8 (with visualization)`

# Difficulty scale of projects

The difficulty field of the issue for the project should map
approximately on the following scale:

- **1: limited project** that doesn't require knowledge of code and
  stays in a single module
  - Nicify prints
  - Small tweaks (such as adding interpolation in the gamelogic)
  - Adding a cvar for a currently constant parameter
- **4: self-contained project** that may require easy interaction with
  other modules and some knowledge of the code
  - Rewriting sound codecs
  - Adding the first implementation of the minimap
  - New hud element
- **7: large project** because of the amount/complexity of the code to
  produce, modules impacted, architectural implications
  - adding IQM
  - Implementing a new alien / weapon / building
  - Rewriting the command system
- **10: big changes**, often architectural. Seriously, before doing one
  of these talk with the rest of the team first
  - making the VMs run in NaCl
  - librocket
  - Bullet