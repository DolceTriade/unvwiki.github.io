---
title: Development environments
permalink: /Development_environments/
---

The purpose of this page is to help developers set up the tools they
need to get work done; basically, research into different tools has been
done here for you.

## Git Front-ends

The official Git project maintains a list of of
[front-ends](http://git-scm.com/downloads/guis).

Some tools offer varying levels of git integration, as well:

- Xcode 4
- QtCreator

## IDEs

Wikipedia has a [comprehensive comparison of C/C++
IDEs](http://en.wikipedia.org/wiki/Comparison_of_integrated_development_environments#C.2FC.2B.2B),
though certain IDEs are better suited for Unvanquished than others.
Specifically, the following are used or have successfully been used by
members of the team:

<table>
<thead>
<tr class="header">
<th><p>Name</p></th>
<th><p>Supported OSes</p></th>
<th><p>Difficulty in setup</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>XCode 4</p></td>
<td><ul>
<li>Mac OS X 10.6+ 32/64-bit<sup>1</sup></li>
<li>Mac OS X 10.7+ 64-bit</li>
</ul></td>
<td><p>Easy</p></td>
</tr>
<tr class="even">
<td><p>QtCreator</p></td>
<td><ul>
<li>Mac OS X<sup>2</sup></li>
<li>Windows</li>
<li>Linux</li>
</ul></td>
<td><ul>
<li>Mac OS X: Easy</li>
<li>Windows: Difficult</li>
<li>Linux: Easy</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Code::Blocks</p></td>
<td><ul>
<li>Mac OS X</li>
<li>Windows</li>
<li>Linux</li>
</ul></td>
<td><ul>
<li>Mac OS X: Easy</li>
<li>Windows: Difficult</li>
<li>Linux: Easy</li>
</ul></td>
</tr>
<tr class="even">
<td><p>Microsoft Visual Studio</p></td>
<td><p>Windows</p></td>
<td></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

Note:

1.  The 32-bit version of XCode 4 for Mac OS X 10.6 and up was only very
    briefly available for Mac OS X some time in early 2011 for a small
    price; following the release of 10.7 (Lion), XCode became freely
    available once more, but only for 64-bit Lion systems.
2.  Builds for older versions of Mac OS X are only available from
    [qt-project.org](http://qt-project.org/downloads), the
    non-commercial Qt project.

## File Comparison Tools

See [Wikipedia's
article](http://en.wikipedia.org/wiki/Comparison_of_file_comparison_tools)
on the subject for a comparison.

### Installing Meld on Windows

Meld is not officially supported for Windows, but can be made to work.

1.  Download and install [Python
    2.7.4](http://www.python.org/ftp/python/2.7.4/python-2.7.4.msi),
    released 6 April 2013. (Newer versions may work as well. A listing
    of [all available downloads](http://www.python.org/ftp/python/) is
    available).
2.  Download and install [PyGtk for
    Windows](http://ftp.gnome.org/pub/GNOME/binaries/win32/pygtk/2.24/pygtk-all-in-one-2.24.2.win32-py2.7.msi)
    (version 2.24.2, released, 9 February 2012).
3.  Download the [latest
    version](http://ftp.gnome.org/pub/GNOME/sources/meld/1.5/meld-1.5.4.tar.xz)
    of Meld, at time of writing version 1.5.4, released 2 April 2012.
    You will need a file decompression tool like
    [7-Zip](http://www.7-zip.org/) to extract the archive. Once
    extracted, for ease of use, you may want to place it in your program
    files directory.
4.  Set the PATH variable to get Python to work:
    1.  Click Start.
    2.  Right click on "Computer" and select "Properties".
    3.  Click "Advanced System Settings" in the sidebar.
    4.  Click "Environment Variables".
    5.  Edit the `PATH` variable and append ";C:\Python27" The semicolon
        acts as a delimiter.

To run Meld, you can use the following:

`> cd "`<var>`path\to\Meld`</var>`\bin"`
`> python meld`

If you would like to create a shortcut, perform the following steps:

1.  Navigate to wherever you extracted your copy of Meld, then to the
    `bin/` subdirectory.
2.  Right click on `meld` and select "Send to" → "Desktop (create
    shortcut)"
3.  On your desktop, right-click on the newly created icon and select
    "Properties".
4.  Prepend the "Target" field with `python`, and click "OK".

## Using vim

### Mac OS X

The easiest (and arguably best) way of getting Vim on Mac OS X is to use
[MacVim](http://code.google.com/p/macvim/), which provides a native Mac
OS X interface that supports most common Mac OS X shortcuts:

| Shortcut         | Action                                                                                                      |
|------------------|-------------------------------------------------------------------------------------------------------------|
| Command-S        | Save the current file.                                                                                      |
| Command-W        | Close the current tab or window.                                                                            |
| Command-O        | Opens a file in a new window.                                                                               |
| Command-Z        | Undoes the last action.                                                                                     |
| Shift-Command-Z  | Redoes the last action.                                                                                     |
| Command-Shift-T  | Opens a file in a new tab.                                                                                  |
| Shift-Command-\[ | Move to the tab left of the current tab, looping around to the rightmost tab if currently at the leftmost.  |
| Shift-Command-\] | Move to the tab right of the current tab, looping around to the leftmost tab if currently at the rightmost. |
|                  |                                                                                                             |

### Installing GLSL syntax files

Download the latest version of the syntax file (`glsl.vim`) from the
[official Vim scripts
page](http://www.vim.org/scripts/script.php?script_id=1002).

Linux and Mac OS X users, place the file in `~/.vim/syntax`. Windows
users, place the file in `%HOMEPATH%\vimfiles\syntax\`.

At this point, users of all systems may edit GLSL files with syntax
highlighting by explicitly setting the filetype to GLSL of the open
file:

`:set syntax=glsl`

For automatic filetype detection, create creating a file with the
following text:

`au BufNewFile,BufRead *.frag,*.vert,*.fp,*.vp,*.glsl setf glsl`

and save it as `~/.vim/ftdetect/glsl.vim` for Mac OS X and Linux users
or `%HOMEPATH%\vimfiles\ftdetect\glsl.vim` for Windows users.

Linux and Mac OS X users may do everything on the command line easily:

`$ mkdir -p ~/.vim/{syntax,ftdetect}`
`$ mv glsl.vim ~/.vim/syntax`
`$ cat > ~/.vim/ftdetect/glsl.vim`
`au BufNewFile,BufRead *.frag,*.vert,*.fp,*.vp,*.glsl setf glsl`
`^d`

Note that `^d` indicates pressing
<span class="key">Control</span>-<span class="key">D</span> on the
keyboard.

### RmlUI highlighting

It's very similar to html/css, so we can ask vim to treat it as such.

`$ echo "au BufNewFile,BufRead *.rml setf html" > ~/.vim/ftdetect/rml.vim`
`$ echo "au BufNewFile,BufRead *.rcss setf css" > ~/.vim/ftdetect/rcss.vim`