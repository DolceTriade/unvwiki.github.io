---
title: Colours
permalink: /Colours/
---

Font colors are used by prefixing text with `^`<var>`char`</var> as
shown in the following table:

| Value       | Color                                                       | Hex         | Floating-point                 |
|-------------|-------------------------------------------------------------|-------------|--------------------------------|
| `0`         | <span style="color:#333333">Dark Grey</span>                | `#333333`   | (`0.2`, `0.2`, `0.2`)          |
| `1`         | <span style="color:#FF0000">Red</span>                      | `#FF0000`   | (`1`, `0`, `0`)                |
| `2`         | <span style="color:#00FF00">Green</span>                    | `#00FF00`   | (`0`, `1`, `0`)                |
| `3`         | <span style="color:#FFFF00">Yellow</span>                   | `#FFFF00`   | (`1`, `1`, `0`)                |
| `4`         | <span style="color:#0000FF">Blue</span>                     | `#0000FF`   | (`0`, `0`, `1`)                |
| `5`         | <span style="color:#00FFFF">Cyan</span>                     | `#00FFFF`   | (`0`, `1`, `1`)                |
| `6`         | <span style="color:#FF00FF">Magenta</span>                  | `#FF00FF`   | (`1`, `0`, `1`)                |
| `7`         | <span style="color:#FFFFFF;">White</span>                   | `#FFFFFF`   | (`1`, `1`, `1`)                |
| `8`         | <span style="color:#FF7F00">Orange</span>                   | `#FF7F00`   | (`1`, `0.5`, `0`)              |
| `9`         | <span style="color:#7F7F7F">Light Grey</span>               | `#7F7F7F`   | (`0.5`, `0.5`, `0.5`)          |
| `:`         | <span style="color:#BFBFBF">Lighter Grey</span>             | `#BFBFBF`   | (`0.75`, `0.75`, `0.75`)       |
| `;`         | <span style="color:#BFBFBF">Lighter Grey[^1]</span>         | `#BFBFBF`   | (`0.75`, `0.75`, `0.75`)       |
| `<`         | <span style="color:#007F00">Forest Green</span>             | `#007F00`   | (`0`, `0.5`, `0`)              |
| `=`         | <span style="color:#7F7F00">Olive Drab</span>               | `#7F7F00`   | (`0.5`, `0.5`, `0`)            |
| `>`         | <span style="color:#00007F">Navy Blue</span>                | `#00007F`   | (`0`, `0`, `0.5`)              |
| `?`         | <span style="color:#7F0000">Maroon</span>                   | `#7F0000`   | (`0.5`, `0`, `0`)              |
| `@`         | <span style="color:#7F3F00">Brown</span>                    | `#7F3F00`   | (`0.5`, `0.25`, `0`)           |
| `A`         | <span style="color:#FF9919">Light Orange</span>             | `#FF9919`   | (`1`, `0.6`, `0.1`)            |
| `B`         | <span style="color:#007F7F">Teal</span>                     | `#007F7F`   | (`0`, `0.5`, `0.5`)            |
| `C`         | <span style="color:#7F007F">Purple</span>                   | `#7F007F`   | (`0.5`, `0`, `0.5`)            |
| `D`         | <span style="color:#007FFF">Baby Blue</span>                | `#007FFF`   | (`0`, `0.5`, `1`)              |
| `E`         | <span style="color:#7F00FF">Periwinkle</span>               | `#7F00FF`   | (`0.5`, `0`, `1`)              |
| `F`         | <span style="color:#3399CC">Turqouise</span>                | `#3399CC`   | (`0.2`, `0.6`, `0.8`)          |
| `G`         | <span style="color:#CCFFCC">Pastel Green</span>             | `#CCFFCC`   | (`0.8`, `1`, `0.8`)            |
| `H`         | <span style="color:#006633">Dark Green</span>               | `#006633`   | (`0`, `0.4`, `0.2`)            |
| `I`         | <span style="color:#FF0033">Firetruck Red</span>            | `#FF0033`   | (`1`, `0`, `0.2`)              |
| `J`         | <span style="color:#B21919">Running out of Names Red</span> | `#B21919`   | (`0.7`, `0.1`, `0.1`)          |
| `K`         | <span style="color:#993300">Dark Red</span>                 | `#993300`   | (`0.6`, `0.2`, `0`)            |
| `L`         | <span style="color:#CC9933">Dark Orange</span>              | `#CC9933`   | (`0.8`, `0.6`, `0.2`)          |
| `M`         | <span style="color:#999933">Beige, Kinda</span>             | `#999933`   | (`0.6`, `0.6`, `0.2`)          |
| `N`         | <span style="color:#FFFFBF">Peach</span>                    | `#FFFFBF`   | (`1`, `1`, `0.75`)             |
| `O`         | <span style="color:#FFFF7F">Light Yellow</span>             | `#FFFF7F`   | (`1`, `1`, `0.5`)              |
| `^`         | Literal `^`                                                 |             |                                |
| `*`         | Reset colour                                                |             |                                |
| `x`*rgb*    | 12 bit hexadecimal RGB notation                             | `#`*rrggbb* | (*r*/15, *g*/15, *b*/15)       |
| `#`*rrggbb* | 24 bit hexadecimal RGB notation                             | `#`*rrggbb* | (*rr*/255, *gg*/255, *bb*/255) |

Anything else, e.g. `^!`, results in both characters being displayed
with no colour change.

For example, entering `^1h^8h^3h^2h^4h^6h` would result in
<span style="color:#FF0000">h</span><span style="color:#FF8000">h</span><span style="color:#FFFF00">h</span><span style="color:#00FF00">h</span><span style="color:#0000FF">h</span><span style="color:#FF00FF">h</span>
being displayed.

<references/>

[^1]: `^;` is reserved for use by the game code. The colour may vary.