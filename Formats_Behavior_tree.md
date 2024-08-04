---
title: Formats Behavior tree
permalink: /Formats/Behavior_tree/
---

Behavior trees file format is game-specific (mods may modify it).

# Introduction

Bot behaviors are decided individually, at each "frame" (read: server's
main loop passage), starting from a root node. Evaluation stops at a
node which returns STATUS_RUNNING, or when the root node returns success
or failure. An overview can be found in the
\[<https://en.wikipedia.org/wiki/Behavior_tree_(artificial_intelligence,_robotics_and_control>)
Wikipedia article\].

# Syntax Reference

Behavior trees use a specific syntax, which obey following rules
(guessed from actual implementation and some C++ readings):

- Each node or leaf returns either `STATUS_SUCCESS`, `STATUS_FAILURE` or
  `STATUS_RUNNING`.
- whitespace has no semantic meaning
- comments (C and C++-style) can either:

:\* start with `//` and go to the end of line

:\* start with `/*` and go to next `*/`, including out of current line.
These do not nest.

- actions and conditions taking parameters must enclose those withing
  parentheses, separated with commas (i.e.
  `roamInRadius( E_H_REACTOR, 500 )`)
- if an action or a condition does not need parameters, parentheses are
  optional
- strings start and end with a double quote `"`
- values can't be stored or modified (additions, subtractions,
  multiplications, etc)
- no user-defined function (but files can be included, and C++ functions
  can be written in the game logic and be used in the behavior tree)
- each possible path should (TODO: verify, even if I fail to understand
  why one would break that willingly) end by one or more action

Note:

It is not possible to do mathematical operations such as additions,
multiplications, divisions, ...

## Keywords

There are several keywords:

- behavior
- action
- sequence
- selector
- fallback
- concurrent
- decorator
- condition

## The `behavior` keyword

`behavior NAME`

Include named behavior at current place. This does not make a new copy
of the referenced tree, so if you include the same behavior more than
once, node-specific state (e.g. timers) will be shared between the
includes.

## The `action` keyword

`action NAME`

`action NAME()`

`action NAME( param )`

`action NAME( param1, param2, ..., paramN )`

Leaves of the tree, they trigger an action from the bot.

### List of actions

Titles provide a link to more detailed pages. TODO: have something more
time-resilient (one page per call, with it's changelog, maybe?)

#### 0.53.1

- activateUpgrade
- aimAtGoal
- alternateStrafe
- buy
- changeGoal
- classDodge
- deactivateUpgrade
- equip
- evolve
- evolveTo
- fight
- fireWeapon
- flee
- gesture
- heal
- jump
- moveInDir
- moveTo
- moveToGoal
- repair
- resetStuckTime
- roam
- roamInRadius
- rush
- say
- strafeDodge
- suicide
- teleport

### Creating new actions

Actions are exported in the `AIActionMap_s AIActions[]` C array. Actions
always return a status. Actions can take a variable number of parameters
(they have minimum and maximum parameter numbers). Parameter types are
not described by API.

##  The `concurrent` keyword

DO NOT USE. It is impossible to have more than one running action, so
there is no known case where this does anything useful.

`concurrent`
`{`
`   NODE_1`
`   NODE_2`
`   ...`
`   NODE_N`
`}`

Concurrent nodes evaluate each children until one returns
`STATUS_FAILURE`. Differences with sequence:

- `STATUS_RUNNING` does not trigger a return
- Returns either `STATUS_SUCCESS` except if one child failed
  `STATUS_FAILURE`.

Notes:

- if 2 tasks were previously in `STATUS_RUNNING` and the 1st returns
  `STATUS_FAILURE`, concurrent returns immediately.

## The `sequence` keyword

`sequence`
`{`
`   NODE_1`
`   NODE_2`
`   ...`
`   NODE_N`
`}`

Sequential nodes evaluate each children one after the other, as long as
they return `STATUS_SUCCESS`. Return last child's status.

- Sequence breaks if a child returns `STATUS_RUNNING`
- Starts at last `STATUS_RUNNING`, if any. Nodes that completed
  successfully in a previous frame are not rerun, as long as the
  sequence is running continually.

## The `selector` keyword

`selector`
`{`
`   NODE_1`
`   NODE_2`
`   ...`
`   NODE_N`
`}`

Selector nodes evaluate each children one after the other, as long as
they return `STATUS_FAILURE`. Return last child's status. Unlike
sequence, this node is stateless: it does not restart from the last
`STATUS_RUNNING`.

## The `fallback` keyword

`fallback`
`{`
`   NODE_1`
`   NODE_2`
`   ...`
`   NODE_N`
`}`

Fallback nodes start by evaluating the first children, and switch to the
next one if a child returns `STATUS_FAILURE`. It will continue from the
last `STATUS_RUNNING` child. Return last child's status.

Difference with sequence:

- Sequence switch to the next child on `STATUS_SUCCESS`, while fallback
  switch to the next child on code\>STATUS_SUCCESS</code>

Difference with selector:

- Starts at last `STATUS_RUNNING`, if any

## The `decorator` keyword

`decorator TYPE( VALUE )`
`{`
`   NODE_1`
`   NODE_2`
`   ...`
`   NODE_N`
`}`

Decorator nodes alters their children's behavior. Decorator types:

- return
- invert
- timer

## The `return` decorator

Force children nodes to return a specific value

## The `invert` decorator

An `invert` node will negate the return value of its node,
<code>STATUS_SUCCESS<code> is turned into `STATUS_FAILURE` and
`STATUS_FAILURE` is turned into `STATUS_SUCCESS`. `STATUS_RUNNING` is
unaffected.

## The `timer` keyword

On encountering a `timer( `<i>`N`</i>` )` node, `STATUS_FAILURE` is
immediately returned if the timer's child node has already returned
`STATUS_FAILURE` within the last N milliseconds.

The node may run more often than every N milliseconds if it keeps
returning success.

## The `condition` keyword

` condition EXPRESSION`

` condition EXPRESSION`
` {`
`   NODE`
` }`
` `

The first form immediately returns *EXPRESSION* as its status:
`STATUS_SUCCESS` for true and `STATUS_FAILURE` for false.

The second form returns `STATUS_FAILURE` if the expression is false, or
otherwise the child's status. Note that *EXPRESSION* is re-evaluated
every frame. If it becomes false at any time during execution of the
child node, the child subtree aborts and the condition node returns
failure.

The idiom

` sequence {`
`   condition EXPRESSION`
`   action myLongRunningAction`
` }`

is used to check a condition once before starting an action, but in
subsequent continue doing the action without re-evaluating the
condition.

Note:

- only executes a single child.
- EXPRESSION can include function calls.

## Operators

Operators are listed in the `AIOpMap_s conditionOps[]` array. operators
sorted by precedence (1st have higher priority):

- "!"
- "\<"
- "\<="
- "\>"
- "\>="
- "=="
- "!="
- "&&"
- "\|\|"

## Functions

Return value is "boxed" (`AIBox`<T>`()`) in the C++ code. Conditions are
exported in the `AIConditionMap_s conditionFuncs[]` array.

### List of functions (as of 0.53.1)

- alertedToEnemy
- aliveTime
- baseRushScore
- buildingIsDamaged
- canEvolveTo
- class
- cvar
- directPathTo
- distanceTo
- goalBuildingType
- goalIsDead
- goalTeam
- goalType
- haveUpgrade
- haveWeapon
- healScore
- inAttackRange
- isVisible
- matchTime
- momentum
- percentAmmo
- percentHealth
- random
- skill
- stuckTime
- team
- teamateHasWeapon
- weapon

## Pre-defined symbols

Some values are pre-defined and usable as action's or function's
parameters.

Those are exported by calling a macro named 'D' (yes, I know). List of
exported symbols:

- human upgrades (including medkit)
- human weapons (excluding blaster)
- team names (aliens, humans, and none)
- alien buildings
- human buildings
- `E_GOAL`
- `E_ENEMY`
- `E_DAMAGEDBUILDING`
- `E_SELF`
- classes (human ones, alien ones, and `PCL_NONE`)
- moves (forward, backward, right, left)
- some say commands (all, team, area, area_team)
- task/check status names (running, success, failure)

## Notes

Parameters needs to be (un)wrapped in C++ before being accessed.

Parameters can be of the following (C) types:

- float
- int (probably better assume 32 bit signed integers)
- string (probably better assume null-terminated)

To provide a value to an action or check, the C++ code must UnBox
(`AIUnBox`<T>`()`) it.

[Category:Formats](Category:Formats "wikilink")
[Category:Bots](Category:Bots "wikilink")