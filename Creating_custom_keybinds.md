---
title: Creating custom keybinds
permalink: /Creating_custom_keybinds/
---

|             |
|-------------|
| __TOC__ |

## Usage

The configuration menus allows to do simple bindings.

For more complicated bindings you need to use the console.

For example you can bind a commands to set a team:

`bind F9 "team a"`
`bind F10 "team h"`

You can also bind a command to set your spawning class, according to
your team:

`// attacking players`
`teambind aliens F5 "class level0"`
`teambind humans F5 "class rifle"`

`// builders`
`teambind aliens F6 "class builderupg builder"`
`teambind humans F6 "class ckit"`

## Differences with Tremulous

A number of commands for keybinds have changed since Tremulous, so
keybind configurations cannot be directly copied from Tremulous to
Unvanquished.

| Tremulous  | Unvanquished | Used for…                                  |
|------------|--------------|--------------------------------------------|
| `+button2` | `+useitem`   | Using an item; granger spit; dragoon barb  |
| `+button3` | `+taunt`     | “Come on!” etc.                            |
| `+button5` | `+attack2`   | Secondary attack                           |
| `+button6` | `+dodge`     | Dodging. NB, this feature has been removed |
| `+button7` | `+activate`  | Using a structure; evolving                |
| `+button8` | `+sprint`    | Sprinting                                  |
|            |              |                                            |

As of alpha 3, the `+button`*`N`* commands are no longer present.

You may want to bind the new [vsays](Voice_say_system "wikilink") to
different keys.

## Gameplay commands

This list was initially populated with commands added after Tremulous
GPP r2259, it may not contain everything and everything listed may not
be useful.

### +activate

Open menu to buy stuff at armoury (humans), open menu to evolve (aliens.

### +attack2

Secondary attack.

### +rally

“Come on!” as in “follow me”.

### +sprint

Run (humans)

### +taunt

“Come on!” as in “bring it on!”.

### buy

<i>(Changed in Alpha 18.)</i> This command can be used with more than
one parameter. The command can also sell items.

|                          |                                                          |
|--------------------------|----------------------------------------------------------|
| `+`<i>`item`</i>         | Sell all which conflicts, then buy `item`.               |
| `-`<i>`item or type`</i> | Sell `item`, or all items of the given type. (See sell.) |
| `?`<i>`item`</i>         | Try to buy `item`, failing quietly.                      |
|                          |                                                          |

For example, if you want a sell-all bind, you would use “<samp>buy -all
rifle</samp>”. This will sell everything you have and buy a rifle.
Anyway if you're prevented to return your construction kit because of
the build timer not having expired yet, the construction kit will not be
returned and the rifle will not be acquired.

### say_area_team

Talk to teammates in the same area (range can be set on server).

### sell

<i>(Changed in Alpha 15.)</i> This command can be used with more than
one parameters.

Special item names:

|                     |                                   |
|---------------------|-----------------------------------|
| `weapon`            | Your current weapon (not blaster) |
| `weapons`           | All weapons                       |
| `upgrades`          | All upgrades                      |
| `armour` or `armor` | All armour items                  |
| `all`               | Everything                        |
|                     |                                   |

### class

This command behaves differently depending on which team you are on.

- As a human or alien, when dead, this command will cause you to spawn
  with the desired class or weapon, respectively.
- As an alien, this command will cause you to evolve to the class
  specified. You may not "evolve" into lower-level classes.

Note that regardless of when you invoke this command, an argument
**must** be supplied or no result will occur.

The following arguments may be used:

| Team   | Argument     | Spawnable? | Availability | Description                                       |
|--------|--------------|------------|--------------|---------------------------------------------------|
| Aliens | `builder`    | Yes        | Stage 1      | [Granger](Granger "wikilink")                     |
|        | `level0`     |            |              | [Dretch](Dretch "wikilink")                       |
|        | `level1`     | No         |              | [Basilisk](Basilisk "wikilink")                   |
|        | `level2`     |            |              | [Marauder](Marauder "wikilink")                   |
|        | `level3`     |            |              | [Dragoon](Dragoon "wikilink")                     |
|        | `builderupg` | Yes        | Stage 2      | [Advanced Granger](Advanced_Granger "wikilink")   |
|        | `level1upg`  | No         |              | [Advanced Basilisk](Advanced_Basilisk "wikilink") |
|        | `level2upg`  |            |              | [Advanced Marauder](Advanced_Marauder "wikilink") |
|        | `level3upg`  |            |              | [Advanced Dragoon](Advanced_Dragoon "wikilink")   |
|        | `level4`     |            | Stage 3      | [Tyrant](Tyrant "wikilink")                       |
| Humans | `rifle`      | Yes        | Stage 1      | [Rifle](Rifle "wikilink")                         |
|        | `ckit`       |            |              | [Construction Kit](Construction_Kit "wikilink")   |
|        |              |            |              |                                                   |

## Configuration commands

### alias

`alias NAME COMMAND [PARAMETERS…]`

Create an alias for the a command with (optional) parameters. The alias
can then be used like if it was a command.

`alias NAME`

Show the command for this alias.

### aliaslist

Lists available command aliases.

### bind

`bind KEY [COMMAND…]` Binds a command or a sequence of commands to this
key, it replaces all existing bindings for that key.

If no command is given it lists the bindings for that key.

### clearaliases

Clears all command aliases.

### cycle

### editbind

`editbind [TEAM] KEY`

Inserts a `/bind` (or `/teambind` command) into the in-game console for
editing. The console is opened if not already opened.

`TEAM` is default, spectators, humans, or aliens. (Initial substrings
are accepted.)

### listrotation

Lists the current map rotation, higlighting the current map.

### loadgame

### message_public

Opens a general chat prompt.

### message_team

Opens a team-chat prompt.

### message_admin

Opens an admin chat prompt.

### message_command

Opens a command prompt.

### modelist

### teambind

`teambind TEAM KEY [COMMAND…]` Binds a command or sequence of commands
to the given key, the bind will only be used when playing on that team.

If command is missing, lists the binding for that key and team.

`TEAM` is default, spectators, humans, or aliens. It's possible to use
initial substrings like *a* for *aliens* or *h* for ''humans.

### toggleConsole

Opens the in-game console (or close it).

### ui_restart

Reloads user interface files.

### unalias

`unalias NAME`

Removes the alias having that name

### unbind

`unbind [TEAM] KEY` Removes all bindings for the given key, or if a TEAM
is given, the binding for the given team on that key.

`TEAM` is default, spectators, humans, or aliens. It's possible to use
initial substrings.

### undelay

### undelayAll

### unregister

Unregister your GUID and name on the server.

## Condition handling

### if condition

`if VALUE CONDITION VALUE THEN [ELSE]`

`if MODIFIERS THEN [ELSE]`

`VALUE` : a variable or number
`CONDITION` : comparison operator
`MODIFIERS` : comma-separated list of keyboard modifiers: Shift, Ctrl, Alt, Command (or Cmd), Mode, Super. Prefix with <kbd>!</kbd> what must not be pressed.
`THEN` and `ELSE` : a variable name or a command string (command string must be prefixed with <kbd>/</kbd> or <kbd>\\</kbd>)

Supported numeric comparison operators:
`= != < <= > >= !=`

Supported string comparison operators:
`eq ne in !in`

The `THEN` clause will be executed, or the `ELSE` clause if present. If
it is a variable name, the content is executed.

For example:

    /if shift "/echo Hello" "/echo Goodbye"
    /bind j "if \$team\$ eq aliens \"/class level1upg level1\""

Notice how the `team` cvar is escaped.

### modcase modifier

`modcase MODIFIERS THEN [MODIFIERS THEN]* [ELSE]`

The leftmost and most-specific `THEN` whose modifier list matches is
executed.

If none match, the `ELSE` is executed if exists.

Let's look at that complex example:

    /modcase shift "/echo 1" ctrl "/echo 2" shift,ctrl "/echo 3" shift,!alt "/echo 4"

The expected behaviour would be:

1.  if Shift and Alt are pressed (clause 4) but not Ctrl (clause 3);
2.  if Ctrl but not Shift are pressed (clause 3);
3.  if Shift and Ctrl are pressed;
4.  if Shift is pressed but neither Alt nor Ctrl.

### strcmp comparison

Take two cvars and compare their string values. *Obsolete.*

## Admin commands

### allready

Switch to the next map without delay. To be used during the
intermission.

### speclock

The player will be prevented from joining a team, this for a given time
or until the end of the current game. The player is moved to spectators
if needed.

### specunlock

Allows a player to join a team if previously locked.

## Utility commands

### calc

Do math calculations on cvars and store the value to a cvar. Useful when
writing scripts.

### concat

Concatenate two cvars into a third.

### delay

### grep

`grep TEXT`

Searches the in-game console history (input and output) for occurrences
of `TEXT` and reprint matching lines.

### help

### math

Do math on cvars. Useful when writing scripts.

### random

Generate a random number

### reloadhud

Reload the HUD without a vid_restart

### screenshotPNG

Saves a screenshot in the PNG format.

### search

`search TEXT`

Searches back through the in-game console for `TEXT` and scrolls to
first occurrence if found.

### searchDown

`searchDown TEXT`

Searches forward through the in-game console for `TEXT` and scrolls to
first occurrence if found.

### snd_reload

Reload sounds (includes a vid_restart

### wav_record

### wav_stoprecord

## Special uses

For commands relevant to development and testing purposes, please see
the [Testing](Testing "wikilink") page.

### buildcubemaps

### cache_endgather

### cache_mapchange

### cache_setindex

### cache_startgather

### cache_usedfile

### fieldinfo

### gameCompleteStatus

### glsl_restart

Triggers recompilation of the GLSL shader code.

### pubkey

Internal use.

### pubkey_identify

Internal use.

### setRecommended

### shaderexp

### spdevmap

Does nothing.

### spmap

Does nothing.

### updatehunkusage

### updatescreen