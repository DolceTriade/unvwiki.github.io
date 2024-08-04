---
title: Modder Documentation: classes .attr.cfg
permalink: /Modder_Documentation:_classes_.attr.cfg/
---

Here are some of the fields present in an
`pkg/unvanquished_src.dpkdir/configs/classes/`***`class`***`.attr.cfg`.

## Metadata

`description "null"`
`icon "null"`
`fovCvar "cg_fov_human"`
`team human`
`unlockThreshold 0`

TODO: document

## Health

here's an *attr.cfg* extract:

`health 100 `
`fallDamage 1.0 `
`regen 0.0`

in it we see:

- `health` how many hp the form have (note that this doesn't work for
  humans as of 0.52.1)
- `fallDamage` how much hp is lost when falling. 1.0 is "as much as a
  normal human". Note that it is also affected by armor if armor is worn
  ("nonloc" damage)
- `regen` how many hp/second are recovered when the creature hasn't been
  hurt for some time

## View

here's an *attr.cfg* extract:

`//View parameters`
`fov 90`
`bob 0.001`
`bobCycle 1.1 `
`stepTime 100 `

TODO: explain

## Movement and mass parameters

here's an *attr.cfg* extract:

`// Physics parameters`
`speed 1.1`
`sprintMod 1.2`
`acceleration 10.0`
`airAcceleration 1.0 `
`friction 7 `
`stopSpeed 100.0`
`jumpMagnitude 170.0`

in it we see:

- `speed` the maximum speed (relative: 1.0 is the speed of a naked
  human)
- `sprintMod` (only makes sense for humans) how much sprinting
  accelerates (relative: 2.0 is the double of the normal `speed`)
- `acceleration` how fast can you change speed while touching the ground
- `airAcceleration` how fast can you change speed while in the air:
  you'll notice that a marauder can easily change direction on the
  ground, but has more trouble steering in the air.
- `friction` how fast is speed lost. Note that if it is high (in the
  hundreds), it will actually limit your max speed noticeably.
- `stopSpeed` means the speed under which the speed will be set to 0.
- `jumpMagnitude` is how high you can jump.

## Abilities

here are some possible values (*attr.cfg* extract):

`// Abilities`
`takesFallDamage`
`canUseLadders`
`wallRunner`
`slider`
`alienSense`
`fovWarps`

TODO: explain

## Stamina (humans)

here's an *attr.cfg* extract:

`// Stamina (per action or second)`
`staminaJumpCost    3750`
`staminaSprintCost  750 `
`staminaJogRestore  750 `
`staminaWalkRestore 2250`
`staminaStopRestore 4500`

in it we see:

- `staminaJumpCost` how much stamina you spend for a jump
- `staminaSprintCost` how much stamina you spend per second when running
- `staminaJogRestore` how fast you recover your stamina (amount per
  second) **while walking but not running**
- `staminaWalkRestore` how fast you recover your stamina (amount per
  second) **while walking slowly or crouching**
- `staminaStopRestore` how fast you recover your stamina (amount per
  second) when not moving

## Miscs

here's an *attr.cfg* extract:

`// Misc`
`cost 200`
`buildDistance 110.0`

in it we see:

- `cost` how much it costs to buy the class or the object. From 0 to
  2000 (for all teams)
- `buildDistance` the maximum distance this form can build (assuming a
  suitable weapon and class)