---
title: Server Map rotation
permalink: /Server/Map_rotation/
---

The `maprotation.cfg` file (in <homepath>`/game/`) holds a
[server's](Server_Running "wikilink") user-defined map rotations.

# Basic Format

This list will indefinitely loop

    maprotation1 {
     plat23
     antares
     vega {
       // execute console commands on mapstart
       cp "Important message for everyone"
     }
     parpax {
       // load the map with one of the layouts
       layouts myfavoritelayout mysecondfavoritelayout
     }
    }

# Advanced Logic

`#label`

Labels are used as location markers. They can be 'seeked' to using a
goto statement:

`goto #label`

For more advanced logic IF statements can be used. `if STATEMENT ACTION`

Where STATEMENT is one of:

- `numClients` (`>` or `<` or `=` ) (number)
- `lastwin` (`aliens` or `humans`)
- `random`

...and ACTION is either a `map` or `label` to `goto`.

Example:

    perseus

    #mainloop
    if numClients > 8 vega
    if numClients < 4 chasm
    spacetracks
    station15

    if lastwin humans #mainloop
    thunder

## Unvanquished 0.55 enhancements

As of Unvanquished 0.55, you will be able to use more operations in `if`
statements and build arbitrary arithmetic and logical expressions. For
example, `if (numClients > 8 && numClients < 12) vega`. The operators
work the same as in C, JavaScript, etc. The supported operators from
lowest precedence to highest are

- `(`...`)` - Grouping with parentheses
- `||` - Logical OR
- `&&` - Logical AND
- `=` or `==` - equals
- `<` - less than, `<=` - less than or equals, `>` - greater than,
  `>=` - greater than or equals
- `+` - addition, `-` - subtraction
- `*` - multiplication, `/` - division, `%` - modulo
- Unary operators: `-` arithmetic negation, `!` - logical NOT

Additionally there are new date and time expressions:

- `time` - hour and minute. 0000 to 2359
- `year` e.g. 2023
- `month` 1-12
- `day` 1-31
- `weekday` - 1 = Sunday, 2 = Monday, ... 7 = Saturday

# Misc Notes

- If you want to reverse a `goto`, use `return`
- `goto` can jump to a label in another rotation, and `resume` will
  return to the last rotation.
- An additional file `default/maprotation.cfg`, in the `unvanquished`
  package, defines the rotation `defaultRotation`.

# Rotation management commands

- `mapRotation `<name> sets the current rotation to <name>.
- `set g_initialMapRotation `<name> can be used to set the rotation on
  server startup (being a cvar, it does not require the gamelogic to be
  running unlike `/mapRotation`).
- `stopRotation` stops any map rotations from running.
- `advanceMapRotation` ???
- `listRotation` shows the active map rotation and the current position
  in it. BUG: does not show the position correctly inside `if` nodes
- `set g_debugMapRotations 1` causes all map rotations to be printed
  upon sgame initialization

[Category:Server](Category:Server "wikilink")
[Category:Formats](Category:Formats "wikilink")