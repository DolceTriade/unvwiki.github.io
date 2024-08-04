---
title: Console
permalink: /Console/
---

Like most quake-derived games, Unvanquished has a drop-down console.
Many game features can only be used via the console, as a
[GUI](https://en.wikipedia.org/wiki/GUI) does not exist for them.

# Basic Usage

Start Unvanquished and open up the console using the **~** (tilde) key
on your keyboard. On US layouts this is below the escape key.

<figure>
<img src="Tilde_key.svg" title="File:Tilde_key.svg" />
<figcaption><a
href="File:Tilde_key.svg">File:Tilde_key.svg</a></figcaption>
</figure>

The console will look like this:

<figure>
<img src="Unvanq_console.png" title="File:Unvanq_console.png" />
<figcaption><a
href="File:Unvanq_console.png">File:Unvanq_console.png</a></figcaption>
</figure>

You can type commands into here and the game will follow them. All
commands are preceded by a backslash:

`/map niveus`
`/kick Veyrdite`
`/ban Kharnov`
`/bot add Bacon humans`

# Tab completion

If you type the first few letters of a command or a asset name, then hit
**TAB** the game will do its best to auto-complete your word for you.
This can also be used for auto-completing map names.

Examples:

`/map niv`**<TAB>**

...would become:

`/map niveus`

`/cg_drawBu`**<TAB>**

...would become:

`/cg_drawBuildableHealth`

If the game cannot work out you want because multiple matches exist,
then it will list all available options for you.

# Key Shortcuts

The in-game console supports many common Unix shortcuts as well as
standard ones:

| Shortcut                                  | Description                                                                                 |
|-------------------------------------------|---------------------------------------------------------------------------------------------|
| PageUp and PageDown, or Shift+ScrollWheel | Scroll up and down in the console history                                                   |
| Ctrl-A                                    | Move the cursor to the start of the line                                                    |
| Ctrl-C or Ctrl-U                          | Clears the current line                                                                     |
| Ctrl-D                                    | Deletes the character in front of the cursor (equivalent to Delete)                         |
| Ctrl-E                                    | Move the cursor to the end of the line                                                      |
| Ctrl-K                                    | Clears to the end of the line                                                               |
| Ctrl-H                                    | Deletes the character behind the cursor (equivalent to Backspace)                           |
| Ctrl-L                                    | Clears the screen                                                                           |
| Ctrl-N                                    | Move forward through console history                                                        |
| Ctrl-P                                    | Move backward through console history                                                       |
| Ctrl-T                                    | Swaps the characters either side of the cursor, then moves the cursor one character forward |
| Ctrl-V                                    | Pastes whatever text is on the clipboard                                                    |
| Ctrl-Home                                 | Scrolls to the top of the console                                                           |
| Ctrl-End                                  | Scrolls to the bottom of the console                                                        |
| Shift-Insert                              | Pastes whatever text is in the X selection buffer                                           |
|                                           |                                                                                             |

# Variable Expansion

Any console variable can be used as an argument to a command by wrapping
said variable between two dollar signs (`$`).

For example, if you were currently spectating and were to type the
following at the console:

`-> say I'm on the $p_teamname$ team!`

everyone on the server would see you say "I'm on the spectator team!".