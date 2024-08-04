---
title: Server Bot skill
permalink: /Server/Bot_skill/
---

This page is a bunch of notes taken while reading the code, and is prone
to errors.

As of commit (between 0.51 and 0.52), bots can have various skill level
between 0 and 9 (10 at least makes bot aim next to their real target).

dist, max_dance and min_dance are shortcuts for:

- DistanceToGoalSquared( self )
- Square( MAX_HUMAN_DANCE_DIST )
- Square( MIN_HUMAN_DANCE_DIST )

Skill level affects:

- aimShake = 10 - skill
- aimSlowness = skill /10
- behaviors:
  - aim prediction time (10 means lesser value, 0 means bigger value)
  - 5 or more: allowed to aim according to target's speed (only for
    lucifer cannon primary attack?)
  - for humans:
    - if not wearing a flamer nor a painsaw, skill above or equal to 3,
      bot distance to goal (not target, goal) \< max_dance, and
      "(distance \> min_dance or skill bellow 5)": backward moves
    - 5 or more: stop sprinting when it would prevent them to jump
      (stamina exhaustion)

[Category:Server](Category:Server "wikilink")