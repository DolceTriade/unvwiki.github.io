---
title: Bot skillset modding
permalink: /Bot_skillset_modding/
---

This wiki page explains the skilltree as of
<https://github.com/Unvanquished/Unvanquished/pull/2635>.

## Basic principle

<figure>
<img src="Bot-skilltree-basic.png" title="Bot-skilltree-basic.png" />
<figcaption>Bot-skilltree-basic.png</figcaption>
</figure>

Each skill is a boolean on/off tag, that has some chance of being
unlocked. As long as there are skill points to spend, the next skill is
selected randomly.

## Visualising the skilltree

There are two commands, `/devbotcountskillpoints` and
`/devbotgraphskilltree [skillLevel]` that can help handling the
skilltree.

The first command, `/devbotcountskillpoints`, just prints a message with
the total cost of (reachable) skills in the tree for each team. This can
help figuring out the maximum budget want.

<figure>
<img src="Bot-skilltree-advanced.png"
title="Bot-skilltree-advanced.png" />
<figcaption>Bot-skilltree-advanced.png</figcaption>
</figure>

The second command, `/devbotgraphskilltree [skillLevel]` saves a `.dot`
graph file that can be converted to an image. For example one can do
this in the game console:

`/devbotgraphskilltree 5`
`game/bot-skilltree-alien.dot written `
`game/bot-skilltree-human.dot written `

Then (e.g.) this in a terminal:

`$ dot -Tpng ~/.local/share/unvanquished/game/bot-skilltree-human.dot > result.png && xdg-open result.png`

If one gives the skill level as an argument argument to the
`/devbotgraphskilltree` command, it will print the statistics for that
skill level, with colors for the disabled and forced skills.

## Modifying and tweaking the skilltree

Depending on your objectives, which maybe to offer diverse and
interesting bots e.g. for a juggernaut mod, or to provide very
predictable bots e.g. for a tournament, you may have different desire
for bot customisations. The current implementation of the skilltree
should be flexible enough to allow this.

The skill selection process is customised by these cvars:

- `g_skillset_baseSkills` which set the initial skills for the various
  skill levels.
- `g_skillset_budgetHumans` and `g_skillset_budgetAliens`
- `g_skillset_disabledSkills`, which will prevent skills from being
  randomly selected.

### Skilltree in pure random "mode"

You sometime want to have maximum randomness in your opponents, with a
purely random skill setup. For example this can make PvE games or
Juggernaut fights more interesting.

You can do that by:

- setting the `g_skillset_baseSkills` cvar to an empty string
- giving some skill funds for your bots to randomly choose from, using
  the `g_skillset_budgetHumans` and `g_skillset_budgetAliens` cvars.

In the current implementation, you get `floor(budget*(2+skillLevel)/9)`
skill points to spend so that the whole budget is unlocked at skill
level 7 while keeping a reasonable amount of points at lower skills. The
code for this is in `src/sgame/sg_bot_skilltree.cpp`, in
`BotPickSkillset`'s definition of `skill_points`.

### Skilltree in pure deterministic "mode"

You sometime want purely deterministic bots, for example for tournaments
or for easier inital balancing. This is the way I'd like Unvanquished to
go towards on the long term.

If you wish to have perfectly identical bots for some skill levels, you
can set `g_skillset_budgetHumans` and `g_skillset_budgetAliens` to 0 and
write the `g_skillset_baseSkills` list.

### Skilltree in mixed "mode"

There is a third way, where one can define "vital" skills that have to
be selected for given skill levels. You can do this by setting the base
skills are always selected, and give more budget than those initial
skills cost, so that the leftover skill points (if any) will be used
randomly.

You can do that by

- setting the `g_skillset_baseSkills` cvar to the base required skills
  for each level, then
- giving some extra skill funds for your bots to randomly choose from,
  using the `g_skillset_budgetHumans` and `g_skillset_budgetAliens`
  cvars.

<b>💡️ Tip:</b> You can even have some skills mandatory at some skill
levels and forbidden from the other skill levels. To do that, you add
the skill in the `g_skillset_disabledSkills` list AND in
`g_skillset_baseSkills` for your desired skill threshold. This will
exclude a skill from the random selection but still allow the budget to
select the other skills. This works because the base skill list takes
precedence.

The visualisation features explained in
[\#Visualising_the_skilltree](#Visualising_the_skilltree "wikilink")
will be very useful in this situation, make sure you know how to use
them.