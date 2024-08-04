---
title: UI Lua in the UI
permalink: /UI/Lua_in_the_UI/
---

Lua scripting can be used in the RmlUi-based UI, similar to how
JavaScript can be used on a web page.

Older versions of the RmlUi library were called libRocket, which
explains the prevalence of the word "Rocket" in the code.

# Documentation resources

The [RmlUi Lua
Manual](https://mikke89.github.io/RmlUiDoc/pages/lua_manual.html) is
useful. Note that the version of RmlUi we are using is out of date.

It's also possible to read the librocket.com documentation in the
Internet Archive/Wayback Machine.

Grepping for examples in the Samples folder (`libs/RmlUi/Samples`) may
be helpful.

Note that these resources are all far from comprehensive. Many Lua
facilities, it seems, can only be discovered by searching the RmlUi
source.

# Tips

The cgame command `luarocket` can be used to execute Lua snippets.
Global variables set from any of the documents are accessible. You can
print things with `print()`.

# Pitfalls

## Bugs

Setting the `inner_rml` attribute of an Element does not work if the
string is longer than 1023 characters.

## Other

All RML documents (or perhaps all documents in a context?) share a
common set of global variables. This means that function names and
global variable names need to be unique across the whole program. Also,
importing a Lua script via `<script src="..." />` in one document
imports it in all documents.

Although Lua usually uses 1-based indexing for arrays, libRocket's Lua
APIs are mostly 0-based. For functions that return a list, this has the
consequence that the length operator `#` returns the wrong result.

[Category:UI](Category:UI "wikilink")