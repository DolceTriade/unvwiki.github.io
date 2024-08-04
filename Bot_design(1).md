---
title: Bot design
permalink: /Bot_design/
---

# Generalities

The main situations we want bots to work in are:

- In a game where a single user plays in a team against a team of bots
  (let's call this *1v0*)
- In a game where a few users play against each others, with a
  considerable amount of bots on both teams (let's call this *1v1, 2v2*,
  etc.)
- In a game where a considerable number of players team up to play
  against a horde of bots (let's call this *PvE*)
- In a game where a single user (or few users) play against a
  considerably bigger number of other users (let's call this *1v3*,
  etc.)

In games where bots are a minority in both teams, bots are not that
important. When playing PvE, the variations of bot skill are also not
very important, as players can't feel like they got an unfairly weak
ally.

Bots are built from roughly 3 different "modules":

- navigation, which is done with a combination of A\* or Dijkstra and
  navmeshes;
- decision, which is done with the paradigm of behavior trees;
- computer vision, to complete what navmeshes can not provide;

## Not a direct part of gameplay

Bots are not a gameplay feature, they are only around to help making
interesting games when there are not enough players around. This means
that it is ok for them to exploit gameplay's weaknesses, by doing things
such as camping, like real players would do. Bots' objective is to win
the game, too, so they should avoid feeding at least at average and
above skill levels.

While they are not a direct part of the gameplay, they still need to
"understand" game's rules as much as possible and adapt to gameplay
changes. For this reason, generic changes should be preferred, in
opposition to hard-coded trigger values (like 0.51's healScore or
baseRushScore, and like current 0.54's GetEnemyPriority).

## Non-cheating

Bots should not perform any action that could not be performed by a
non-bot client. Bots currently cheat in few cases, because of technical
and historical reasons. However, this is un-desired status and
considered as bugs (see details in next §). This property does take some
care to maintain, as bot functions often act directly on sgame state
rather than using client commands.

It would be nice if additionally, bots only used *information* that
could have been learned by a normal player. This is far from true in the
current state: for example, bots have omniscience of the closest (in
ghost distance) buildable of each type in the level, which also applies
to friends and foes..

When playing against bots, it should not *feel* like a bot is cheating,
i.e. doing something that a human player could not have done. The bot
should not have impossibly fast reaction times or seem like it's using
an aimbot, triggerbot, etc.

# Navigation

All bots should be able to reach any part of the map that does not
require special training.

## Computer vision

Bots should be able to detect any enemy in their FoV. It would be nice
to have bots not being too good at finding hidden buildables on the
roof. This makes hiding eggs unfun and next to impossible in the current
state. Unless they are placed outside of a navmesh, in which case bots
are totally unable to discover them.

To improve this and make bots feel more like human players, we should
make bots:

- not automatically know the egg locations when rushing:
  <https://github.com/Unvanquished/Unvanquished/pull/2683>
- attack enemies that are visible but outside the navmesh
- for human bots, not be as great at spotting things vertically as they
  are with thing horizontally (like regular humans)
- maybe not discovering things always with the same reliability — but
  this would bring randomness.

# Decision

## Bot levels

For historical reasons, bots have a range of skills numbered from 1 to
9, all integers.

Skill 1 is considered to be training dummies.

Skill 5 should never be so strong that an average player can not kill it
in duel, nor so weak than an average player considers the bot
negligible.

Skill 9 should be made as hard as possible.

In some cases, bots currently cheat (they "smell" enemy buildings
depending on some conditions) . This is because of technical limitations
of the code infrastructure, but is not desired.

# Bot personalities

In 2022 and early 2023, we did some experiments about giving each bot a
personality. The idea was to have a number of skills that are valuable
in playing. Each bot would receive its unique set of skills, by some
random selection. That would make them different from each other.

Some examples of "bot skills" we used are: various alien trick moves,
the ability to aim better than other bots, smartly buying human
equipment/weapons and using the human medkit.

The pros of this approach:

- Bots do not behave all the same. That makes them more difficult to
  predict.
- Bots simulate real users more accurately.

The cons:

- It is harder to balance bots against each other. We would have to test
  a significant subset of all possible combinations. This matters a lot
  in 1v1 or 2v2. It matters even more in 1v3.
- Users will discover what skills are more valuable. They can tweak the
  skills the bots on their team have, by voting to remove them and add
  them again until they hit a sweet spot.

Those two cons should be mitigated by having sufficiently many skills
and skills that have well adapted costs: that is by having costs reflect
the skill's usefulness.

## Distributing Skills over Bot Levels

Let *All* denote the set of all bot skills. Let *S1, S2, ..., S9* denote
the sets of skills given to each level from 1 to 9. We should aim for
*S1* ⊆ *S2* ⊆ ... ⊆ *S9* = *All*.

As of May 2023, we have:

    All = {
        aim-barbs,
        aim-head,
        buy-modern-armor,
        fast-aim,
        feels-pain,
        flee-run,
        goon-attack-jump,
        goon-flee-jump,
        mantis-attack-jump,
        mantis-flee-jump,
        mara-attack-jump,
        mara-flee-jump,
        medkit,
        predict-aim,
        prefer-armor,
        safe-barbs,
        small-attack-jump,
        strafe-attack,
        tyrant-attack-run,
        tyrant-flee-run
    }

There is also `movement, fighting`, which seem to be a little
mysterious.

This table summarizes the proposed skills for each level:

| Level | Skills                                                                                 |
|-------|----------------------------------------------------------------------------------------|
| S1    | {prefer-armor, medkit}                                                                 |
| S2    | S1                                                                                     |
| S3    | S2 ∪ {strafe-attack}                                                                   |
| S4    | S3                                                                                     |
| S5    | S4 ∪ {aim-barbs, feels-pain, flee-run, \*-attack-jump, \*-flee-jump, buy-modern-armor} |
| S6    | S5                                                                                     |
| S7    | S6 ∪ {aim-head, predict-aim, safe-barbs}                                               |
| S8    | S7                                                                                     |
| S9    | S8                                                                                     |

# Current Questions

- Should we keep bot personalities, or make all bots the same?
- How much randomness should be involved in a bot's behavior?
- How many details of bot configuration should be hard-coded, and how
  many should be exposed by cvars?