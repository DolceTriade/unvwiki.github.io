---
title: Wiki Editing Guidelines
permalink: /Wiki_Editing_Guidelines/
---

## Editing reference

The [official MediaWiki
documentation](http://www.mediawiki.org/wiki/Help:Editing_pages) and
[Wikipedia's
documentation](http://en.wikipedia.org/wiki/Help:Getting_started) are
the most helpful, but pages can at times be difficult to find.

- [MediaWiki's editing cheat
  sheet](http://www.mediawiki.org/wiki/Help:Formatting)
- [Wikipedia's editing cheat
  sheet](http://en.wikipedia.org/wiki/Wikipedia:Cheatsheet)
- [Using images](http://www.mediawiki.org/wiki/Help:Images)
  - [Fixing SVGs](http://en.wikipedia.org/wiki/Wikipedia:SVG_Help) for
    the wiki
- [Using lists](http://meta.wikimedia.org/wiki/Help:List)
- [Using tables](http://meta.wikimedia.org/wiki/Help:Table)
- [Using
  formulas](http://en.wikipedia.org/wiki/Help:Displaying_a_formula)
  (This is also a handy LaTeX reference.)

## Best practices

- **Do** host images on the wiki as opposed to third-party sites.
- **Do** spell-check your work before submitting changes.
- **Do** write change summaries.
- **Do** try to make similar pages visually consistent.
- **Do** consider creating
  [templates](http://www.mediawiki.org/wiki/Help:Templates) when markup
  becomes redundant.
- **Do** capitalize the names of human weapons, buildables, and upgrades
  when the names are names and not just descriptions. E.g., "battery
  pack" could be left as-is, but "Lucifer cannon" or "Lucifer Cannon"
  are preferred over "lucifer cannon".
- **Do not** use lossy image formats for shots of player classes,
  weapons, and upgrades.
- **Do not** link to the same page as you are editing.
- **Do not** link to a page that has already been recently linked to.
- **Do not** use horizontal rules to delimit list items.
- **Avoid** redundancy with the page title in section titles.
- **Do not** unnecessarily bold text.
- **Do not** use colons in section titles.
- **Do not** capitalize the initial of a noun, even if it is something
  game-related.
- **Do not** use abbreviated names in image filenames. For example,
  write "Reactor.png" instead of "Rc.png".
- **Do not** include the GUI or HUD in screenshots of items or weapons.
  Disable them by setting `cg_draw2D` to 0.
- **Do not** use preformatted text blocks for anything other than
  preformatted text. Preformatted text blocks are defined by indenting
  text by one or more characters, and are typically used for code or
  console displays.

## Tables

Tables can be formatted in the wiki syntax:

     {| style="wikitable
     |-
     ! Heading 1
     ! Heading 2
     |-

     | Row 1
     | Item 1
     |-

     | Row 2 of the table
     | Another item
     |-

     |}

... or in the HTML syntax:

     <table>
     <tr>
       <td> Interesting information </td>
       <td> Anime </td>
     </tr>
     </table>

Use which ever option that you think will make the page source easier to
read for new editors.

- **Don't** use *colspan* or *rowspan* unless absolutely necessary —
  they make understanding and editing table source codes much harder
- **Beware** tables without a style will lay your information out but
  not draw borders around it.

# Best Image Guidelines

Although bandwidth is not an issue for the server, image-heavy pages are
a pain to load for most users. Keeping sizes down while ensuring no
visible quality issues is advised.

In *almost* every case you should only be using one of three image
formats for this wiki:

- PNG
- JPEG with quality around 85 to 90
- SVG

If you need a better quality JPEG, then consider using PNG instead. The
JPEG quality scale gives exponentially rising file size for
exponentially lowering extra quality as you increase the Q number. For
final images, quality 85-90 is approximately the line where artefacts
start becoming visible for most people.

**Do** host a second lossless copy of images you may think need both
lossy (for pages) and lossless (for further editing) variants. **Do
not** use formats such as:

- webp
- jpeg2000
- gif
- mng
- bmp
- etc

... because they are either inefficient compared to JPG and PNG *or* not
supported by the majority of web browsers.