---
title: Tools Archipelago
permalink: /Tools/Archipelago/
---

In authoring 3d models, there exists a number of problems associated
with the immutability of a model that has been unwrapped and textured:

- If all the available texture space has been used, additional geometry
  cannot be added to the model without the use of another texture sheet.
- If the model's texturing spans multiple texture sheets, those sheets
  cannot easily be combined.
- UV islands cannot be rearranged once the model has been textured
  without also manipulating the corresponding texture data. With a
  modern rendering architecture, that would require rearranging islands
  of quite a few textures: a model might have diffuse, normal, glow,
  specular intensity, and specular color maps, for example.

This page describes the design for a tool that would facilitate
rearranging islands of a completed model and the texture data at the
same time, while being responsive and non-destructive during the editing
process.

## Usage

The workflow would be as follows:

1.  The user exports a model from their modeling application of choice
    to the Wavefront .obj format.
2.  The user launches the remapping tool by whatever means in their
    (modern) web browser of choice.
3.  The user rearranges islands at their leisure. Islands on one texture
    sheet may be moved to any other texture sheet (but may not cross
    sheet boundaries).

## Loading files

1.  [The .obj file is parsed.](#Parsing_data "wikilink")
2.  [UV islands are identified.](#Identifying_islands "wikilink")
3.  [UV islands are displayed.](#Displaying_islands "wikilink")
4.  [Texture files are loaded on an as-needed
    basis.](#Displaying_islands "wikilink")

## Implementation

The application will be written in SVG using CSS and JavaScript. XHTML
(via the tag) may be used as well. This approach is highly
cross-platform.

### Targeted browsers

- — Fully supported.

- — Fully supported.

- — Fully supported.

- — Needs investigation.

- — Versions prior to 9 will not be supported, but may end up working.
  Version 9 will likely not be supported with the first release.

## Milestones

### Milestone 1: Implement most of base classes

Base classes include:

-

- — An analogue to 2x3 [SVG transform
  matrices](http://www.w3.org/TR/SVG/coords.html#TransformAttribute).

  -

- (only parsing facilities)

  -

  -

- (only parsing facilities)

-

- — Initializes everything associated with the application.

- — An abstraction for the DOM `window` class.

- — An abstraction for the mouse (which is not present as a DOM class).

- — A radio button style control.

### Milestone 2: Implement (most of) the GUI

-

- -

  -

- - Perhaps instead of a specific design as we have now, we should
    create a generic `Panel` class out of which this class is made.

  -

### Milestone 3: Implement UV island detection

- — A data representation of a UV island.

### Milestone 4: Implement file I/O

- — Provides an interface to the user for selecting a file (by some
  means).

- — Abstraction for reading files.

- — Abstraction for writing files.

- — Performs an XMLHttpRequest.

These classes are to simplify the process of selecting, reading, and
writing files, and to ensure that the application will always have some
level of usability (on supported browsers); even if the user is on
Internet Explorer which currently lacks File API support, for example,
they will be able to at least copy and paste data into and out of the
program (or use some other workaround).

## User Interface Design Questions

### User interface help

- Aside from documentation, what sort of help do we provide to the user?
  -

  - How do we inform the user from within the application of keyboard
    shortcuts?
    -

### Saving & Loading

- How do we differentiate between project files and .obj files? I.e., do
  we have separate import and open functions? Do we even have a project
  file format?
- How does the user save their work?
  - Do we use a proprietary format to save the user's progress, or do we
    just save the final product?
  - Do we auto-save so that the user can recover from a browser crash?
- How does the user load a file to work on?
  - If the File API is supported, we should use that to select a file.
  - How does the user begin a new editing session when a file is already
    being worked on?
- What do we do when the program cannot load a file?

### Manipulating UV islands

- Do we allow showing/hiding UV islands?
  - If so, what would the GUI be like? Would we just use Blender-style
    shortcuts?
- Do we allow Blender-style shortcuts?
- Do we allow selecting and manipulating multiple islands?
  - If we do, do we have an undo history for selection operations?
- Do we create user interface controls entirely with SVG geometry or do
  we use XHTML?
  - Using XHTML requires the tag, [which is not supported in
    IE9](http://schmerg.com/svg-support-in-ie9-close-but-should-try-harde).
    Because the objective is to generate the user interface using
    JavaScript, user interface DOM elements are abstracted by classes,
    so it should not be a problem to support both. For the first
    release, IE9 will therefore not be targeted as using XHTML is easier
    for a number of controls (e.g., combo boxes).

### Texture sheet display

- Are islands shown (initially) 1:1 with the users' monitor, or are they
  scaled to fit the screen?
- Do we allow zooming in and out?
- If we allow zooming in or showing the islands 1:1 with the users'
  monitor, which would create the possibility that the texture sheets
  extend beyond the view space,
  - How does the user pan the view around?
  - Is the user permitted to pan beyond the edge of the image?

## File I/O, Crash prevention

### Preventing crashes by actively saving the users' work

There are four mechanisms potentially available to us:

- `document.cookie` — Write the users' work to a cookie. This might not
  work as we can't make any expectations as to what the users' browser
  will let us do here, and how permanent these cookies will be.
- hidden — Hide a textarea element on the document, and as the user
  works, periodically write the users' work in text form to the text
  area; some browsers have facilities to "remember" what was in the text
  area. **This is an awful hack.** This likely could not be created
  using JavaScript but would have to be a part of the document markup.
- `window.localStorage` — An HTML5 technology. Worth looking into.
- `FileWriter` — Performed using our abstraction class, `UnvFileWriter`,
  if supported.

### Reading files

The following options are present, in order of preference:

- File API
- Create a text area (either on the same page or in a popup window) for
  the user to manually paste into.
- Java applet (ala TiddlyWiki's tiddlysaver.jar).
- Browser extension

### Writing files

The following options are present, in order of preference:

- File API
- Put data in the user's clipboard for them to manually paste into a
  text file.
- Put data in a text area (either on the same page or in a popup window)
  for the user to manually copy and paste into a text file.
- Java applet (ala TiddlyWiki's tiddlysaver.jar).
- Browser extension

As for rendering the final textures, we may also use the tags' rendering
feature, but this would be slow for a model with many textures to
render.

### What needs to be written

- Edited textures
- Updated material files (.mtl)?
- Updated mesh file (.obj)

## Parsing data

For ease of parsing, we will use the [Wavefront .obj
format](http://en.wikipedia.org/wiki/Wavefront_.obj_file) and its
associated [.mtl material
format](http://en.wikipedia.org/wiki/Wavefront_.obj_file#Material_template_library).

Both vertex and material data is parsed in the same way:

- Read a line.
- Strip extraneous whitespace and comments.
- Parse keywords. Throw an error if the keyword is unknown.

## Identifying islands

1.  Identify which UV coordinates are used by which faces.
2.  Identify which faces share edges.
3.  Identify contiguous regions of faces:
    1.  Select a random vertex.
    2.  For each edge sharing that vertex, add those vertices to the
        selection.
    3.  Repeat the previous step using each of those newly selected
        vertices, stopping when the number of selected vertices does not
        increase. This is one island.
    4.  Repeat steps 1–3 using a vertex that has not been selected yet.

## Displaying islands

Once islands have been identified,

1.  Calculate triangle adjacency data.
2.  Identify edges that are at the perimeter or a hole (edges that used
    by only one triangle).
3.  Generate an SVG path with the edge loops (including hole edge
    loops).
4.  Apply a pattern to the path.

To make holes appear as such, we'll set the `fill-rule` property to
[`evenodd`](http://www.w3.org/TR/SVG/painting.html#FillProperties).

Islands are filled using s created on an as-needed basis for each
texture. Toggling which texture is displayed could be done one of two
ways:

1.  **Set the fill for each island using that DOM element's
    `.style.fill` member.** When the display mode is changed, iterate
    over every island and change said attribute. If `id`s associated
    with each texture were differentiated by suffixes (i.e.., all
    glowmaps would end in "_glow", all diffuse maps would end in
    "_diffuse", etc.), a regular expression could be used to replace
    the suffix of each fill with the suffix associated with the new
    display mode.
2.  **Set the class of each island to one corresponding to its
    texture.** That is, each texture would have its own class. When the
    display mode is changed, the fill of each class would be changed and
    the browser would take care of updating the display of the islands.

The latter seems quite a bit simpler to implement.

## Manipulating islands

There are three methods we could implement (which are not mutually
exclusive; i.e., two or three could be implemented):

1.  Only islands which are selected can be modified. Islands are
    selected in the usual manner, by clicking and using modifier keys.
2.  Islands are modified without selection; they are selected by mousing
    over them (like sloppy focus in a WM).

<table>
<thead>
<tr class="header">
<th style="width:0px"></th>
<th style="width:50%"><p>Click to select</p></th>
<th style="width:50%"><p>Mouse over to select</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="padding:0px 10px"><p>Pros</p></td>
<td><ul>
<li>Manipulating multiple islands at once is possible.</li>
</ul></td>
<td><ul>
<li>Manipulating individual islands becomes very quick.</li>
</ul></td>
</tr>
<tr class="even">
<td style="padding:0px 10px"><p>Cons</p></td>
<td><ul>
<li>Makes moving many islands quickly slower as there is the additional
step(s) of selecting and deselecting.</li>
</ul></td>
<td><ul>
<li>Manipulating multiple islands at once is impossible.</li>
</ul></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

### With keyboard shortcuts

#### Selection manipulation

| Shortcut | Action                                                                                                                                                                                                |
|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| a        | Select all if nothing is selected or deselect all if there is currently a selection.                                                                                                                  |
| c        | Select islands by "painting" with a circular "brush". When this mode is active, the size of the "brush" is increased by scrolling the mouse wheel down and decreased by scrolling the mouse wheel up. |
| b        | Select islands using a rectangular marquee.                                                                                                                                                           |
|          |                                                                                                                                                                                                       |

#### Island manipulation

| Shortcut     | Action                                                       |
|--------------|--------------------------------------------------------------|
| g            | Move an island.                                              |
| s            | Scale an island.                                             |
| r            | Rotate an island.                                            |
| Manipulators |                                                              |
| Shift        | Slow movement by some linear factor to make it more precise. |
| Ctrl         | Snap movement to grid squares.                               |
|              |                                                              |

## Coordinate spaces

### Displaying multiple texture sheets

Multiple texture sheets are shown adjacent to one another.

## GUI Design

### Features to add

- Menus
- Flip toolbar to bottom/top
- Option to show/hide toolbar button labels

### Icons

- File I/O
  - — Image of an open file folder.

  - — Image of a floppy disk.
- Manipulators
  - — Arrows pointing up, down, left, and right from center.

  -

  - — Image of a square with a larger, dotted square behind it.
- Display modes
  - — A checkerboard pattern overlaid onto a circle.

  -

  - — A greyscale image of a plane with a step in it.

  - — Three overlapping red, green, and blue circles, with Venn-like
    color combinations between them.

  - — An image of a green, glowing mesh.

  - — A circle that appears to be glowing red.

  - — A circle with gradients typical of a normal map.

  - — A greyscale pseudo-sphere (circle) with a shiny spot.

  - — A colorful pseudo-sphere (circle) with a shiny spot.
- Miscellaneous
  - — We may be able to use a Unicode checkmark (CHECK MARK U+2713 or
    HEAVY CHECK MARK U+2714) for this.

It might make more sense to use squares rather than circles for some
icons as that would give more room or allow conveying information that
would otherwise be difficult.

## Resources

### foreignObject

- [MDN docs on the
  subject](https://developer.mozilla.org/en-US/docs/SVG/Element/foreignObject)
- [A demo of it in
  action](http://ajaxian.com/archives/foreignobject-hey-youve-got-html-in-my-svg)

### AJAX

- [Using the right version of MSXML in Internet
  Explorer](http://blogs.msdn.com/b/xmlteam/archive/2006/10/23/using-the-right-version-of-msxml-in-internet-explorer.aspx)
  (official MSDN docs)

### File API

- [Official W3C Specification](http://www.w3.org/TR/FileAPI/)
- [MDN
  documentation](https://developer.mozilla.org/en-US/docs/Using_files_from_web_applications)
- [Microsoft's analysis of the
  API](http://html5labs.interoperabilitybridges.com/prototypes/fileapi/fileapi/info)
- [A discussion on the current state of File API
  implementations](http://www.filosophy.org/post/27/a_state_of_limbo_the_html5_file_api_filereader_and_blobs/)f
- [How gmail uses the File
  API](http://www.thecssninja.com/javascript/gmail-upload)
- [Current support for the File API on different
  browsers](http://caniuse.com/fileapi)

[Category:Tools](Category:Tools "wikilink")