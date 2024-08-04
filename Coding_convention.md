---
title: Coding convention
permalink: /Coding_convention/
---

This is the style guide for Unvanquished's and Daemon's source code.

The first rule of style is to follow the style of the surrounding code.
If there is a clear convention in the local region of code, continue to
use it (with the possible exception of "Obsolete conventions" below).
There are two broadly used style conventions, whose particularities are
described in the "Quake style" and "New style" sections below.

See also [Reformatting the source](Reformatting_the_source "wikilink")
and [Coding with intrinsics](Coding_with_intrinsics "wikilink").

## Spacing

There is a space between a control structure keyword (e.g. `while`) and
the following `(`, if applicable.

The curly braces surrounding class, struct, and function definitions go
on their own lines.

Consider adding breaking the line if the line is longer than 100
characters (assuming tab width 4?).

Control blocks without braces are discouraged. If you need an if
followed by only one line use something like that:

    if ( foo )
    {
        bar;
    }

## Naming conventions

- Function names (including member functions) and class names are
  `CamelCase`.
- Variable and function argument names are `camelCase`.
- Struct data members are `camelCase`.
- Class data members are `camelCase_` (with a trailing underscore).

Functions that are used by other files have a "namespace" of some kind,
either a C++ namespace, or a prefix like `G_` or `FS_`. Follow the style
of the surrounding code.

Functions that are only used within the same file are marked `static`
and need not have a namespace.

## Other trivialities

- When defining a type alias, use `using A = B;`, not `typedef B A;`.

<!-- -->

- Declare variables as close to the point of first use as possible.

<!-- -->

- Do not write `void` in the parentheses of functions that take zero
  arguments.

<!-- -->

- Always use `override` for member functions that override a virtual
  member function.

<!-- -->

- `struct` is usually used for structures that have only public fields
  and no member functions. `class` is usually used for structures that
  have at least one private member and at least one member function.

  Do not add member functions to structs that have a large number of
  fields and a poorly defined scope of responsibility.

## Quake style

This style is found in files inherited from Tremulous (and often further
from Quake 3).

- There is always a space after `(` or `[` and before `)` or `]`, EXCEPT
  when the parentheses or brackets are empty.
- The curly braces `{ }` of control structures always go on their own
  lines.
- File names are `snake_case.cpp`

### Obsolete conventions

These conventions are often found in Quake-style files, but are
**discouraged** even for new code in those files.

- Function banner comments, like this:
      /*
      ================
      GL_TextureMode
      ================
      */

  There is no need to write the name of a function in a comment
  preceding it. Documentation about what the function does or how it is
  implemented is of course welcome.
- All local variables declared at the beginning of the function. This
  exists because old C compilers required variables to be declared at
  the beginning.
- Vertical alignment in lists of function declarations or variable
  declarations, e.g.
      foo    varName;
      foobar varName2;

## New style

This style is commonly found in the BSD-licensed files in Daemon (which
are often more-recently created ones). Although it is "new", that does
not necessarily mean it is better; many contributors prefer the Quake
style.

- No space after `(` or `[`, nor before `)` or `]`.
- The opening `{` of a control structure goes on the same line as the
  `if`/`else`/`while`/etc.
- File names are `CamelCase.cpp`

## Assertions, self-documentation and dependency reduction

- When a function takes a pointer as parameter, if this pointer should
  never be NULL, use an assertion to test it. (Or use a reference
  instead?) It helps at debugging, but also to document the code.
- When a function takes a pointer to a struct for read-only access,
  please mark it as a const pointer.
- If a function only needs a subpart of a struct, pass only that subpart
  (by example, if you only use gentity_t-\>playerState_t, only give it a
  playerState_t\*)

## Refactoring

when refactoring, if you need to guarantee elements to be accessed
together, move them in sub-class. This will help keep consistency with
old code while allowing to progressively modernize codebase. New classes
should have theirs own headers and implementation files (explicitly
listed in the CMakeLists.txt), except if small.

### Function and API evolutions

Some changes are usually desired, but might have bad side effects like
performance cost or different behaviors. Here is a small list of those:

- prefer `Str::IsEqual` and `Str::IsIEqual` to `Q_stricmp` or `strcmp`.
  Those need to size of the strings though, which might impact
  performances in a non negligible (and bad) way.
- prefer to use glm instead of the old Quake vector API (vec3_t,
  VectorCopy, VectorMA</code>, etc) when possible. But keep in mind that
  `glm::normalize( v )` will not handle cases where v have components
  values of zero.